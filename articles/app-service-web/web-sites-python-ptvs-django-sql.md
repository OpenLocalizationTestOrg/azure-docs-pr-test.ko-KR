---
title: "Azure의 Django 및 SQL 데이터베이스와 Python Tools 2.2 for Visual Studio"
description: "Python Tools for Visual Studio를 사용하여 SQL 데이터베이스 인스턴스에 데이터를 저장하고 Azure 앱 서비스 웹앱에 배포할 수 있는 Django 웹앱을 만드는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 65b59dee2b7bddca77d31c692dab713c68d67e24
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="django-and-sql-database-on-azure-with-python-tools-22-for-visual-studio"></a><span data-ttu-id="e0595-103">Azure의 Django 및 SQL 데이터베이스와 Python Tools 2.2 for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e0595-103">Django and SQL Database on Azure with Python Tools 2.2 for Visual Studio</span></span>
<span data-ttu-id="e0595-104">이 자습서에서는 PTVS 샘플 템플릿 중 하나를 사용하여 간단한 설문 조사 웹앱을 만들기 위해 [Python Tools for Visual Studio] 를 사용해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="e0595-104">In this tutorial, we'll use [Python Tools for Visual Studio] to create a simple polls web app using one of the PTVS sample templates.</span></span> <span data-ttu-id="e0595-105">이 자습서는 [비디오](https://www.youtube.com/watch?v=ZwcoGcIeHF4)로도 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0595-105">This tutorial is also available as a [video](https://www.youtube.com/watch?v=ZwcoGcIeHF4).</span></span>

<span data-ttu-id="e0595-106">Azure에서 호스트된 SQL 데이터베이스를 사용하는 방법, SQL을 사용하도록 웹앱을 구성하는 방법 및 [Azure 앱 서비스 웹앱](http://go.microsoft.com/fwlink/?LinkId=529714)에 웹앱을 게시하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="e0595-106">We'll learn how to use a SQL database hosted on Azure, how to configure the web app to use a SQL database, and how to publish the web app to [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

<span data-ttu-id="e0595-107">Bottle, Flask 및 Django 웹 프레임워크, Azure 테이블 저장소, MySQL 및 SQL 데이터베이스 서비스를 사용하여 PTVS로 Azure 앱 서비스 웹앱을 개발하는 내용을 다루는 추가 문서에 대해서는 [Python 개발자 센터] 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e0595-107">See the [Python Developer Center] for more articles that cover development of Azure App Service Web Apps with PTVS using Bottle, Flask and Django web frameworks, with Azure Table Storage, MySQL and SQL Database services.</span></span> <span data-ttu-id="e0595-108">이 문서는 앱 서비스를 중점적으로 다루지만 포함된 단계는 [Azure 클라우드 서비스]를 개발할 때와 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="e0595-108">While this article focuses on App Service, the steps are similar when developing [Azure Cloud Services].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e0595-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="e0595-109">Prerequisites</span></span>
* <span data-ttu-id="e0595-110">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="e0595-110">Visual Studio 2015</span></span>
* <span data-ttu-id="e0595-111">[Python 2.7 32비트]</span><span class="sxs-lookup"><span data-stu-id="e0595-111">[Python 2.7 32-bit]</span></span>
* <span data-ttu-id="e0595-112">[Python Tools 2.2 for Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="e0595-112">[Python Tools 2.2 for Visual Studio]</span></span>
* <span data-ttu-id="e0595-113">[Python Tools 2.2 for Visual Studio Samples VSIX]</span><span class="sxs-lookup"><span data-stu-id="e0595-113">[Python Tools 2.2 for Visual Studio Samples VSIX]</span></span>
* <span data-ttu-id="e0595-114">[Azure SDK Tools for VS 2015]</span><span class="sxs-lookup"><span data-stu-id="e0595-114">[Azure SDK Tools for VS 2015]</span></span>
* <span data-ttu-id="e0595-115">Django 1.9 이상</span><span class="sxs-lookup"><span data-stu-id="e0595-115">Django 1.9 or later</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="e0595-116">Azure 계정을 등록하기 전에 Azure App Service를 시작하려면 [App Service 체험](https://azure.microsoft.com/try/app-service/)으로 이동합니다. App Service에서 단기 스타터 웹앱을 즉시 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0595-116">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="e0595-117">신용 카드는 필요하지 않으며 약정도 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e0595-117">No credit cards required; no commitments.</span></span>
>
>

## <a name="create-the-project"></a><span data-ttu-id="e0595-118">프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="e0595-118">Create the Project</span></span>
<span data-ttu-id="e0595-119">이 섹션에서는 샘플 템플릿을 사용하여 Visual Studio 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e0595-119">In this section, we'll create a Visual Studio project using a sample template.</span></span> <span data-ttu-id="e0595-120">가상 환경을 만들고 필요한 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="e0595-120">We'll create a virtual environment and install required packages.</span></span> <span data-ttu-id="e0595-121">sqlite를 사용하여 로컬 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e0595-121">We'll create a local database using sqlite.</span></span> <span data-ttu-id="e0595-122">그런 다음 웹앱을 로컬로 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e0595-122">Then we'll run the web app locally.</span></span>

1. <span data-ttu-id="e0595-123">Visual Studio에서 **파일**, **새 프로젝트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e0595-123">In Visual Studio, select **File**, **New Project**.</span></span>
2. <span data-ttu-id="e0595-124">[Python Tools 2.2 for Visual Studio Samples VSIX]의 프로젝트 템플릿은 **Python**, **샘플**에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0595-124">The project templates from the [Python Tools 2.2 for Visual Studio Samples VSIX] are available under **Python**, **Samples**.</span></span> <span data-ttu-id="e0595-125">**Polls Django Web Project** 를 선택하고 확인을 클릭하여 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e0595-125">Select **Polls Django Web Project** and click OK to create the project.</span></span>

     ![새 프로젝트 대화 상자](./media/web-sites-python-ptvs-django-sql/PollsDjangoNewProject.png)
3. <span data-ttu-id="e0595-127">외부 패키지를 설치할지 묻는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0595-127">You will be prompted to install external packages.</span></span> <span data-ttu-id="e0595-128">**가상 환경에 설치**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e0595-128">Select **Install into a virtual environment**.</span></span>

     ![외부 패키지 대화 상자](./media/web-sites-python-ptvs-django-sql/PollsDjangoExternalPackages.png)
4. <span data-ttu-id="e0595-130">기본 해석기로 **Python 2.7** 을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e0595-130">Select **Python 2.7** as the base interpreter.</span></span>

     ![가상 환경 추가 대화 상자](./media/web-sites-python-ptvs-django-sql/PollsCommonAddVirtualEnv.png)
5. <span data-ttu-id="e0595-132">**솔루션 탐색기**에서 프로젝트 노드를 마우스 오른쪽 단추로 클릭하고 **Python**을 선택한 다음 **Django Migrate**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e0595-132">In **Solution Explorer**, right-click on the project node and select **Python**, and then select **Django Migrate**.</span></span>  <span data-ttu-id="e0595-133">그런 다음 **Django Create Superuser**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e0595-133">Then select **Django Create Superuser**.</span></span>
6. <span data-ttu-id="e0595-134">Django 관리 콘솔이 열리고 프로젝트 폴더에 sqlite 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e0595-134">This will open a Django Management Console and create a sqlite database in the project folder.</span></span> <span data-ttu-id="e0595-135">프롬프트에 따라 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e0595-135">Follow the prompts to create a user.</span></span>
7. <span data-ttu-id="e0595-136"><kbd>F5</kbd> 키를 눌러 응용프로그램이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e0595-136">Confirm that the application works by pressing <kbd>F5</kbd>.</span></span>
8. <span data-ttu-id="e0595-137">위쪽의 탐색 모음에서 **로그인** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e0595-137">Click **Log in** from the navigation bar at the top.</span></span>

     ![웹 브라우저](./media/web-sites-python-ptvs-django-sql/PollsDjangoCommonBrowserLocalMenu.png)
9. <span data-ttu-id="e0595-139">데이터베이스를 동기화할 때 만든 사용자의 자격 증명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e0595-139">Enter the credentials for the user you created when you synchronized the database.</span></span>

     ![웹 브라우저](./media/web-sites-python-ptvs-django-sql/PollsDjangoCommonBrowserLocalLogin.png)
10. <span data-ttu-id="e0595-141">**Create Sample Polls**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e0595-141">Click **Create Sample Polls**.</span></span>

      ![웹 브라우저](./media/web-sites-python-ptvs-django-sql/PollsDjangoCommonBrowserNoPolls.png)
11. <span data-ttu-id="e0595-143">poll and vote를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e0595-143">Click on a poll and vote.</span></span>

      ![웹 브라우저](./media/web-sites-python-ptvs-django-sql/PollsDjangoSqliteBrowser.png)

## <a name="create-a-sql-database"></a><span data-ttu-id="e0595-145">SQL 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="e0595-145">Create a SQL Database</span></span>
<span data-ttu-id="e0595-146">데이터베이스에 대해 Azure SQL 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e0595-146">For the database, we'll create an Azure SQL database.</span></span>

<span data-ttu-id="e0595-147">다음 단계에 따라 데이터베이스를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0595-147">You can create a database by following these steps.</span></span>

1. <span data-ttu-id="e0595-148">[Azure 포털]에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="e0595-148">Log into the [Azure Portal].</span></span>
2. <span data-ttu-id="e0595-149">탐색 창 맨 아래쪽에서 **새로 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e0595-149">At the bottom of the navigation pane, click **NEW**.</span></span> <span data-ttu-id="e0595-150">**데이터 + 저장소** > **SQL Database**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e0595-150">, click **Data + Storage** > **SQL Database**.</span></span>
3. <span data-ttu-id="e0595-151">새 리소스 그룹을 만들어 새 SQL 데이터베이스를 구성하고 적절한 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e0595-151">Configure the new SQL Database by creating a new resource group and select the appropriate location for it.</span></span>
4. <span data-ttu-id="e0595-152">SQL 데이터베이스를 만든 후 데이터베이스 블레이드에서 **Visual Studio에서 열기** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e0595-152">Once the SQL Database is created, click **Open in Visual Studio** in the database blade.</span></span>
5. <span data-ttu-id="e0595-153">**방화벽 구성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e0595-153">Click **Configure your firewall**.</span></span>
6. <span data-ttu-id="e0595-154">**방화벽 설정** 블레이드에서 **시작 IP** 및 **종료 IP**를 개발 컴퓨터의 공용 IP 주소로 설정하여 방화벽 규칙을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e0595-154">In the **Firewall Settings** blade, add a firewall rule with **START IP** and **END IP** set to the public IP address of your development machine.</span></span> <span data-ttu-id="e0595-155">**저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e0595-155">Click **Save**.</span></span>

   <span data-ttu-id="e0595-156">개발 컴퓨터에서 데이터베이스 서버에 연결할 수 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0595-156">This will allow connections to the database server from your development machine.</span></span>
7. <span data-ttu-id="e0595-157">데이터베이스 블레이드로 돌아가서 **속성**을 클릭하고 **데이터베이스 연결 문자열 표시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e0595-157">Back in the database blade, click **Properties**, then click **Show database connection strings**.</span></span>
8. <span data-ttu-id="e0595-158">복사 단추를 사용하여 **ADO.NET** 값을 클립보드에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="e0595-158">Use the copy button to put the value of **ADO.NET** on the clipboard.</span></span>

## <a name="configure-the-project"></a><span data-ttu-id="e0595-159">프로젝트 구성</span><span class="sxs-lookup"><span data-stu-id="e0595-159">Configure the Project</span></span>
<span data-ttu-id="e0595-160">이 섹션에서는 방금 만든 SQL 데이터베이스를 사용하도록 웹앱을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="e0595-160">In this section, we'll configure our web app to use the SQL database we just created.</span></span> <span data-ttu-id="e0595-161">Django에서 SQL 데이터베이스를 사용하는 데 필요한 추가 Python 패키지도 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="e0595-161">We'll also install additional Python packages required to use SQL databases with Django.</span></span> <span data-ttu-id="e0595-162">그런 다음 웹앱을 로컬로 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e0595-162">Then we'll run the web app locally.</span></span>

1. <span data-ttu-id="e0595-163">Visual Studio에서 **ProjectName**폴더의 *settings.py* 를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e0595-163">In Visual Studio, open **settings.py**, from the *ProjectName* folder.</span></span> <span data-ttu-id="e0595-164">일시적으로 연결 문자열을 편집기에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="e0595-164">Temporarily paste the connection string in the editor.</span></span> <span data-ttu-id="e0595-165">연결 문자열은 다음 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="e0595-165">The connection string is in this format:</span></span>

       Server=<ServerName>,<ServerPort>;Database=<DatabaseName>;User ID=<UserName>;Password={your_password_here};Encrypt=True;TrustServerCertificate=False;Connection Timeout=30;

<span data-ttu-id="e0595-166">위의 값을 사용하도록 `DATABASES` 의 정의를 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="e0595-166">Edit the definition of `DATABASES` to use the values above.</span></span>

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

1. <span data-ttu-id="e0595-167">솔루션 탐색기의 **Python Environments**에서 가상 환경을 마우스 오른쪽 단추로 클릭하고 **Install Python Package**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e0595-167">In Solution Explorer, under **Python Environments**, right-click on the virtual environment and select **Install Python Package**.</span></span>
2. <span data-ttu-id="e0595-168">**pip**를 사용하여 패키지 `pyodbc`를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="e0595-168">Install the package `pyodbc` using **pip**.</span></span>

     ![Python 패키지 설치 대화 상자](./media/web-sites-python-ptvs-django-sql/PollsDjangoSqlInstallPackagePyodbc.png)
3. <span data-ttu-id="e0595-170">**pip**를 사용하여 패키지 `django-pyodbc-azure`를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="e0595-170">Install the package `django-pyodbc-azure` using **pip**.</span></span>

     ![Python 패키지 설치 대화 상자](./media/web-sites-python-ptvs-django-sql/PollsDjangoSqlInstallPackageDjangoPyodbcAzure.png)
4. <span data-ttu-id="e0595-172">**솔루션 탐색기**에서 프로젝트 노드를 마우스 오른쪽 단추로 클릭하고 **Python**을 선택한 다음 **Django Migrate**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e0595-172">In **Solution Explorer**, right-click on the project node and select **Python**, and then select **Django Migrate**.</span></span>  <span data-ttu-id="e0595-173">그런 다음 **Django Create Superuser**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e0595-173">Then select **Django Create Superuser**.</span></span>

   <span data-ttu-id="e0595-174">이렇게 하면 이전 섹션에서 만든 SQL 데이터베이스에 대한 테이블이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="e0595-174">This will create the tables for the SQL database we created in the previous section.</span></span> <span data-ttu-id="e0595-175">프롬프트에 따라 사용자를 만듭니다. 이 사용자가 첫 번째 섹션에서 만든 sqlite 데이터베이스의 사용자와 일치할 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e0595-175">Follow the prompts to create a user, which doesn't have to match the user in the sqlite database created in the first section.</span></span>
5. <span data-ttu-id="e0595-176">`F5`키를 눌러 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e0595-176">Run the application with `F5`.</span></span> <span data-ttu-id="e0595-177">**Create Sample Polls** 를 사용하여 만든 설문 조사와 투표를 통해 제출된 데이터는 SQL 데이터베이스에서 serialize됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0595-177">Polls that are created with **Create Sample Polls** and the data submitted by voting will be serialized in the SQL database.</span></span>

## <a name="publish-the-web-app-to-azure-app-service"></a><span data-ttu-id="e0595-178">Azure 앱 서비스에 웹앱 게시</span><span class="sxs-lookup"><span data-stu-id="e0595-178">Publish the web app to Azure App Service</span></span>
<span data-ttu-id="e0595-179">Azure .NET SDK를 통해 Azure 앱 서비스 웹앱에 웹앱을 쉽게 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0595-179">The Azure .NET SDK provides an easy way to deploy your web web app to Azure App Service Web Apps.</span></span>

1. <span data-ttu-id="e0595-180">**솔루션 탐색기**에서 프로젝트 노드를 마우스 오른쪽 단추로 클릭하고 **게시**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e0595-180">In **Solution Explorer**, right-click on the project node and select **Publish**.</span></span>

     ![웹 게시 대화 상자](./media/web-sites-python-ptvs-django-sql/PollsCommonPublishWebSiteDialog.png)
2. <span data-ttu-id="e0595-182">**Microsoft Azure 웹앱**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e0595-182">Click on **Microsoft Azure Web Apps**.</span></span>
3. <span data-ttu-id="e0595-183">**새로 만들기** 를 클릭하여 새 웹앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e0595-183">Click on **New** to create a new web app.</span></span>
4. <span data-ttu-id="e0595-184">다음 필드에 입력하고 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e0595-184">Fill in the following fields and click **Create**.</span></span>

   * <span data-ttu-id="e0595-185">**웹앱 이름**</span><span class="sxs-lookup"><span data-stu-id="e0595-185">**Web App name**</span></span>
   * <span data-ttu-id="e0595-186">**앱 서비스 계획**</span><span class="sxs-lookup"><span data-stu-id="e0595-186">**App Service plan**</span></span>
   * <span data-ttu-id="e0595-187">**리소스 그룹**</span><span class="sxs-lookup"><span data-stu-id="e0595-187">**Resource group**</span></span>
   * <span data-ttu-id="e0595-188">**지역**</span><span class="sxs-lookup"><span data-stu-id="e0595-188">**Region**</span></span>
   * <span data-ttu-id="e0595-189">**데이터베이스 서버**를 **데이터베이스 없음**으로 그대로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e0595-189">Leave **Database server** set to **No database**</span></span>
5. <span data-ttu-id="e0595-190">다른 모든 기본값을 그대로 적용하고 **게시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e0595-190">Accept all other defaults and click **Publish**.</span></span>
6. <span data-ttu-id="e0595-191">웹 브라우저가 자동으로 게시된 웹앱으로 열립니다.</span><span class="sxs-lookup"><span data-stu-id="e0595-191">Your web browser will open automatically to the published web app.</span></span> <span data-ttu-id="e0595-192">Azure에 호스트된 **SQL** 데이터베이스를 사용하여 예상한 대로 웹앱이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e0595-192">You should see the web app working as expected, using the **SQL** database hosted on Azure.</span></span>

   <span data-ttu-id="e0595-193">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="e0595-193">Congratulations!</span></span>

     ![웹 브라우저](./media/web-sites-python-ptvs-django-sql/PollsDjangoAzureBrowser.png)

## <a name="next-steps"></a><span data-ttu-id="e0595-195">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e0595-195">Next steps</span></span>
<span data-ttu-id="e0595-196">Python Tools for Visual Studio, Django and SQL 및 SQL 데이터베이스에 대해 자세히 알아보려면 다음 링크를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e0595-196">Follow these links to learn more about Python Tools for Visual Studio, Django and SQL Database.</span></span>

* <span data-ttu-id="e0595-197">[Python Tools for Visual Studio 설명서]</span><span class="sxs-lookup"><span data-stu-id="e0595-197">[Python Tools for Visual Studio Documentation]</span></span>
  * <span data-ttu-id="e0595-198">[웹 프로젝트]</span><span class="sxs-lookup"><span data-stu-id="e0595-198">[Web Projects]</span></span>
  * <span data-ttu-id="e0595-199">[클라우드 서비스 프로젝트]</span><span class="sxs-lookup"><span data-stu-id="e0595-199">[Cloud Service Projects]</span></span>
  * <span data-ttu-id="e0595-200">[Microsoft Azure의 원격 디버깅]</span><span class="sxs-lookup"><span data-stu-id="e0595-200">[Remote Debugging on Microsoft Azure]</span></span>
* <span data-ttu-id="e0595-201">[Django 설명서]</span><span class="sxs-lookup"><span data-stu-id="e0595-201">[Django Documentation]</span></span>
* <span data-ttu-id="e0595-202">[SQL 데이터베이스]</span><span class="sxs-lookup"><span data-stu-id="e0595-202">[SQL Database]</span></span>

## <a name="whats-changed"></a><span data-ttu-id="e0595-203">변경된 내용</span><span class="sxs-lookup"><span data-stu-id="e0595-203">What's changed</span></span>
* <span data-ttu-id="e0595-204">웹 사이트에서 앱 서비스로의 변경에 대한 지침은 [Azure 앱 서비스와 이 서비스가 기존 Azure 서비스에 미치는 영향](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="e0595-204">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!--Link references-->
<span data-ttu-id="e0595-205">[Python 개발자 센터]: /develop/python/</span><span class="sxs-lookup"><span data-stu-id="e0595-205">[Python Developer Center]: /develop/python/</span></span>
<span data-ttu-id="e0595-206">[Azure 클라우드 서비스]: ../cloud-services/cloud-services-python-ptvs.md</span><span class="sxs-lookup"><span data-stu-id="e0595-206">[Azure Cloud Services]: ../cloud-services/cloud-services-python-ptvs.md</span></span>

<!--External Link references-->
<span data-ttu-id="e0595-207">[Azure 포털]: https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="e0595-207">[Azure Portal]: https://portal.azure.com</span></span>
<span data-ttu-id="e0595-208">[Python Tools for Visual Studio]: http://aka.ms/ptvs</span><span class="sxs-lookup"><span data-stu-id="e0595-208">[Python Tools for Visual Studio]: http://aka.ms/ptvs</span></span>
<span data-ttu-id="e0595-209">[Python Tools 2.2 for Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025</span><span class="sxs-lookup"><span data-stu-id="e0595-209">[Python Tools 2.2 for Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025</span></span>
<span data-ttu-id="e0595-210">[Python Tools 2.2 for Visual Studio Samples VSIX]: http://go.microsoft.com/fwlink/?LinkID=624025</span><span class="sxs-lookup"><span data-stu-id="e0595-210">[Python Tools 2.2 for Visual Studio Samples VSIX]: http://go.microsoft.com/fwlink/?LinkID=624025</span></span>
<span data-ttu-id="e0595-211">[Azure SDK Tools for VS 2015]: http://go.microsoft.com/fwlink/?LinkId=518003</span><span class="sxs-lookup"><span data-stu-id="e0595-211">[Azure SDK Tools for VS 2015]: http://go.microsoft.com/fwlink/?LinkId=518003</span></span>
<span data-ttu-id="e0595-212">[Python 2.7 32비트]: http://go.microsoft.com/fwlink/?LinkId=517190</span><span class="sxs-lookup"><span data-stu-id="e0595-212">[Python 2.7 32-bit]: http://go.microsoft.com/fwlink/?LinkId=517190</span></span>
<span data-ttu-id="e0595-213">[Python Tools for Visual Studio 설명서]: http://aka.ms/ptvsdocs</span><span class="sxs-lookup"><span data-stu-id="e0595-213">[Python Tools for Visual Studio Documentation]: http://aka.ms/ptvsdocs</span></span>
<span data-ttu-id="e0595-214">[Microsoft Azure의 원격 디버깅]: http://go.microsoft.com/fwlink/?LinkId=624026</span><span class="sxs-lookup"><span data-stu-id="e0595-214">[Remote Debugging on Microsoft Azure]: http://go.microsoft.com/fwlink/?LinkId=624026</span></span>
<span data-ttu-id="e0595-215">[웹 프로젝트]: http://go.microsoft.com/fwlink/?LinkId=624027</span><span class="sxs-lookup"><span data-stu-id="e0595-215">[Web Projects]: http://go.microsoft.com/fwlink/?LinkId=624027</span></span>
<span data-ttu-id="e0595-216">[클라우드 서비스 프로젝트]: http://go.microsoft.com/fwlink/?LinkId=624028</span><span class="sxs-lookup"><span data-stu-id="e0595-216">[Cloud Service Projects]: http://go.microsoft.com/fwlink/?LinkId=624028</span></span>
<span data-ttu-id="e0595-217">[Django 설명서]: https://www.djangoproject.com/</span><span class="sxs-lookup"><span data-stu-id="e0595-217">[Django Documentation]: https://www.djangoproject.com/</span></span>
<span data-ttu-id="e0595-218">[SQL 데이터베이스]: /documentation/services/sql-database/</span><span class="sxs-lookup"><span data-stu-id="e0595-218">[SQL Database]: /documentation/services/sql-database/</span></span>
