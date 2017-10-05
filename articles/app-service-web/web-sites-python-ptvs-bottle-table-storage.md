---
title: "Azure의 Bottle 및 Azure 테이블 저장소와 Python Tools 2.2 for Visual Studio"
description: "Python Tools for Visual Studio를 사용하여 Azure 테이블 저장소에서 데이터를 저장하는 Bottle 응용 프로그램을 만들고 웹앱을 Azure 앱 서비스 웹앱에 배포하는 방법을 알아봅니다."
services: app-service\web
documentationcenter: python
author: huguesv
manager: erikre
editor: 
ms.assetid: f075124b-db79-4e51-b394-09187dd6c634
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 07/07/2016
ms.author: huvalo
ms.openlocfilehash: fb25f03607ac6e9af46b47f54e830e0283dd1b0a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="bottle-and-azure-table-storage-on-azure-with-python-tools-22-for-visual-studio"></a><span data-ttu-id="8f954-103">Azure의 Bottle 및 Azure 테이블 저장소와 Python Tools 2.2 for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="8f954-103">Bottle and Azure Table Storage on Azure with Python Tools 2.2 for Visual Studio</span></span>
<span data-ttu-id="8f954-104">이 자습서에서는 PTVS 샘플 템플릿 중 하나를 사용하여 간단한 설문 조사 웹앱을 만들기 위해 [Python Tools for Visual Studio] 를 사용해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="8f954-104">In this tutorial, we'll use [Python Tools for Visual Studio] to create a simple polls web app using one of the PTVS sample templates.</span></span> <span data-ttu-id="8f954-105">이 자습서는 [비디오](https://www.youtube.com/watch?v=GJXDGaEPy94)로도 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="8f954-105">This tutorial is also available as a [video](https://www.youtube.com/watch?v=GJXDGaEPy94).</span></span>

<span data-ttu-id="8f954-106">설문 조사 웹앱은 리포지토리의 추상화를 정의하므로 여러 다른 유형의 리포지토리(메모리 내, Azure 테이블 저장소, MongoDB) 간을 쉽게 전환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f954-106">The polls web app defines an abstraction for its repository, so you can easily switch between different types of repositories (In-Memory, Azure Table Storage, MongoDB).</span></span>

<span data-ttu-id="8f954-107">Azure 저장소 계정을 만드는 방법, Azure 테이블 저장소를 사용하도록 웹앱을 구성하는 방법 및 [Azure 앱 서비스 웹앱](http://go.microsoft.com/fwlink/?LinkId=529714)에 웹앱을 게시하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="8f954-107">We'll learn how to create an Azure Storage account, how to configure the web app to use Azure Table Storage, and how to publish the web app to [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

<span data-ttu-id="8f954-108">Bottle, Flask 및 Django 웹 프레임워크, MongoDB, Azure 테이블 저장소, MySQL 및 SQL 데이터베이스 서비스를 사용하여 PTVS로 Azure 앱 서비스 웹앱을 개발하는 내용을 다루는 추가 문서에 대해서는 [Python 개발자 센터] 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8f954-108">See the [Python Developer Center] for more articles that cover development of Azure App Service Web Apps with PTVS using Bottle, Flask and Django web frameworks, with MongoDB, Azure Table Storage, MySQL and SQL Database services.</span></span> <span data-ttu-id="8f954-109">이 문서는 앱 서비스를 중점적으로 다루지만 포함된 단계는 [Azure 클라우드 서비스]를 개발할 때와 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="8f954-109">While this article focuses on App Service, the steps are similar when developing [Azure Cloud Services].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8f954-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="8f954-110">Prerequisites</span></span>
* <span data-ttu-id="8f954-111">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="8f954-111">Visual Studio 2015</span></span>
* <span data-ttu-id="8f954-112">[Python Tools 2.2 for Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="8f954-112">[Python Tools 2.2 for Visual Studio]</span></span>
* <span data-ttu-id="8f954-113">[Python Tools 2.2 for Visual Studio Samples VSIX]</span><span class="sxs-lookup"><span data-stu-id="8f954-113">[Python Tools 2.2 for Visual Studio Samples VSIX]</span></span>
* <span data-ttu-id="8f954-114">[Azure SDK Tools for VS 2015]</span><span class="sxs-lookup"><span data-stu-id="8f954-114">[Azure SDK Tools for VS 2015]</span></span>
* <span data-ttu-id="8f954-115">[Python 2.7 32비트] 또는 [Python 3.4 32비트]</span><span class="sxs-lookup"><span data-stu-id="8f954-115">[Python 2.7 32-bit] or [Python 3.4 32-bit]</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="8f954-116">Azure 계정을 등록하기 전에 Azure App Service를 시작하려면 [App Service 체험](https://azure.microsoft.com/try/app-service/)으로 이동합니다. App Service에서 단기 스타터 웹앱을 즉시 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f954-116">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="8f954-117">신용 카드는 필요하지 않으며 약정도 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8f954-117">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="create-the-project"></a><span data-ttu-id="8f954-118">프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="8f954-118">Create the Project</span></span>
<span data-ttu-id="8f954-119">이 섹션에서는 샘플 템플릿을 사용하여 Visual Studio 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8f954-119">In this section, we'll create a Visual Studio project using a sample template.</span></span> <span data-ttu-id="8f954-120">가상 환경을 만들고 필요한 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="8f954-120">We'll create a virtual environment and install required packages.</span></span> <span data-ttu-id="8f954-121">그런 후 기본 메모리 내 리포지토리를 사용하여 로컬로 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="8f954-121">Then we'll run the application locally using the default in-memory repository.</span></span>

1. <span data-ttu-id="8f954-122">Visual Studio에서 **파일**, **새 프로젝트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8f954-122">In Visual Studio, select **File**, **New Project**.</span></span>
2. <span data-ttu-id="8f954-123">[Python Tools 2.2 for Visual Studio Samples VSIX]의 프로젝트 템플릿은 **Python**, **샘플**에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f954-123">The project templates from the [Python Tools 2.2 for Visual Studio Samples VSIX] are available under **Python**, **Samples**.</span></span> <span data-ttu-id="8f954-124">**Polls Bottle Web Project** 를 선택하고 확인을 클릭하여 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8f954-124">Select **Polls Bottle Web Project** and click OK to create the project.</span></span>
   
     ![새 프로젝트 대화 상자](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleNewProject.png)
3. <span data-ttu-id="8f954-126">외부 패키지를 설치할지 묻는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8f954-126">You will be prompted to install external packages.</span></span> <span data-ttu-id="8f954-127">**가상 환경에 설치**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8f954-127">Select **Install into a virtual environment**.</span></span>
   
     ![외부 패키지 대화 상자](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleExternalPackages.png)
4. <span data-ttu-id="8f954-129">기본 해석기로 **Python 2.7** 또는 **Python 3.4**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8f954-129">Select **Python 2.7** or **Python 3.4** as the base interpreter.</span></span>
   
     ![가상 환경 추가 대화 상자](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonAddVirtualEnv.png)
5. <span data-ttu-id="8f954-131">`F5`키를 눌러 응용 프로그램이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="8f954-131">Confirm that the application works by pressing `F5`.</span></span> <span data-ttu-id="8f954-132">기본적으로 응용 프로그램은 구성이 필요하지 않은 메모리 내 리포지토리를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8f954-132">By default, the application uses an in-memory repository which doesn't require any configuration.</span></span> <span data-ttu-id="8f954-133">따라서 웹 서버가 중지되면 모든 데이터가 손실됩니다.</span><span class="sxs-lookup"><span data-stu-id="8f954-133">All data is lost when the web server is stopped.</span></span>
6. <span data-ttu-id="8f954-134">**Create Sample Polls**를 클릭하고 poll and vote를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8f954-134">Click **Create Sample Polls**, then click on a poll and vote.</span></span>
   
     ![웹 브라우저](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleInMemoryBrowser.png)

## <a name="create-an-azure-storage-account"></a><span data-ttu-id="8f954-136">Azure 저장소 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="8f954-136">Create an Azure Storage Account</span></span>
<span data-ttu-id="8f954-137">저장소 작업을 사용하려면 Azure 저장소 계정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="8f954-137">To use storage operations, you need an Azure storage account.</span></span> <span data-ttu-id="8f954-138">다음 단계에 따라 저장소 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f954-138">You can create a storage account by following these steps.</span></span>

1. <span data-ttu-id="8f954-139">[Azure Portal](https://portal.azure.com/)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="8f954-139">Log into the [Azure Portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="8f954-140">포털의 왼쪽 위에서 **새로 만들기** 아이콘을 클릭한 다음 **데이터 + 저장소** > **저장소 계정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8f954-140">Click the **New** icon on the top left of the Portal, then click **Data + Storage** > **Storage Account**.</span></span>  <span data-ttu-id="8f954-141">**만들기** 단추를 클릭하고 저장소 계정에 고유한 이름을 지정한 다음 이를 위한 새 [리소스 그룹](../azure-resource-manager/resource-group-overview.md)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8f954-141">Click the **Create** button, then give the storage account a unique name and create a new [resource group](../azure-resource-manager/resource-group-overview.md) for it.</span></span>
   
      ![빠른 생성](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonAzureStorageCreate.png)
   
    <span data-ttu-id="8f954-143">저장소 계정이 만들어지면 **알림** 단추가 녹색 **성공**으로 깜박이고 저장소 계정의 블레이드가 열려 새로 만든 리소스 그룹에 속한 것을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="8f954-143">When the storage account has been created, the **Notifications** button will flash a green **SUCCESS** and the storage account's blade is open to show that it belongs to the new resource group you created.</span></span>
3. <span data-ttu-id="8f954-144">저장소 계정 블레이드에서 **액세스 키** 부분을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8f954-144">Click the **Access keys** part in the storage account's blade.</span></span> <span data-ttu-id="8f954-145">계정 이름 및 key1을 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="8f954-145">Take note of the account name and key1.</span></span>
   
      ![구성](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonAzureStorageKeys.png)
   
    <span data-ttu-id="8f954-147">다음 섹션에서 프로젝트를 구성하려면 이 정보가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="8f954-147">We will need this information to configure your project in the next section.</span></span>

## <a name="configure-the-project"></a><span data-ttu-id="8f954-148">프로젝트 구성</span><span class="sxs-lookup"><span data-stu-id="8f954-148">Configure the Project</span></span>
<span data-ttu-id="8f954-149">이 섹션에서는 방금 만든 저장소 계정을 사용하도록 응용 프로그램을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="8f954-149">In this section, we'll configure our application to use the storage account we just created.</span></span> <span data-ttu-id="8f954-150">그런 후 응용 프로그램을 로컬로 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="8f954-150">Then we'll run the application locally.</span></span>

1. <span data-ttu-id="8f954-151">Visual Studio의 솔루션 탐색기에서 프로젝트 노드를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8f954-151">In Visual Studio, right-click on your project node in Solution Explorer and select **Properties**.</span></span> <span data-ttu-id="8f954-152">**디버그** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8f954-152">Click on the **Debug** tab.</span></span>
   
     ![프로젝트 디버그 설정](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleAzureTableStorageProjectDebugSettings.png)
2. <span data-ttu-id="8f954-154">**서버 명령 디버그**, **환경**에서 응용 프로그램에 필요한 환경 변수 값을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="8f954-154">Set the values of environment variables required by the application in **Debug Server Command**, **Environment**.</span></span>
   
       REPOSITORY_NAME=azuretablestorage
       STORAGE_NAME=<storage account name>
       STORAGE_KEY=<primary access key>
   
   <span data-ttu-id="8f954-155">이렇게 하면 **디버깅 시작**을 사용할 때 환경 변수가 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="8f954-155">This will set the environment variables when you **Start Debugging**.</span></span> <span data-ttu-id="8f954-156">**디버깅하지 않고 시작**을 사용할 때 해당 변수를 설정하려면 **서버 명령 실행**에서도 동일한 값을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="8f954-156">If you want the variables to be set when you **Start Without Debugging**, set the same values under **Run Server Command** as well.</span></span>
   
   <span data-ttu-id="8f954-157">또는 Windows 제어판을 사용하여 환경 변수를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f954-157">Alternatively, you can define environment variables using the Windows Control Panel.</span></span> <span data-ttu-id="8f954-158">소스 코드/프로젝트 파일에 자격 증명을 저장하지 않으려는 경우에는 이 방법이 더 나은 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="8f954-158">This is a better option if you want to avoid storing credentials in source code / project file.</span></span> <span data-ttu-id="8f954-159">응용 프로그램에서 새 환경 값이 사용되려면 Visual Studio를 다시 시작해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f954-159">Note that you will need to restart Visual Studio for the new environment values to be available to the application.</span></span>
3. <span data-ttu-id="8f954-160">Azure 테이블 저장소 리포지토리를 구현하는 코드는 **models/azuretablestorage.py**에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f954-160">The code that implements the Azure Table Storage repository is in **models/azuretablestorage.py**.</span></span> <span data-ttu-id="8f954-161">Python의 테이블 서비스를 사용하는 방법에 대한 자세한 내용은 [설명서] 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8f954-161">See the [documentation] for more information on how to use Table Service from Python.</span></span>
4. <span data-ttu-id="8f954-162">`F5`키를 눌러 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="8f954-162">Run the application with `F5`.</span></span> <span data-ttu-id="8f954-163">**Create Sample Polls** 를 사용하여 만든 설문 조사와 투표를 통해 제출된 데이터는 Azure 테이블 저장소에서 serialize됩니다.</span><span class="sxs-lookup"><span data-stu-id="8f954-163">Polls that are created with **Create Sample Polls** and the data submitted by voting will be serialized in Azure Table Storage.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="8f954-164">Python 2.7 가상 환경에는 Visual Studio에서 예외 나누기가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f954-164">The Python 2.7 Virtual Environment may cause an exception break in Visual Studio.</span></span>  <span data-ttu-id="8f954-165">`F5` 키를 눌러 웹 프로젝트를 계속 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="8f954-165">Press `F5` to continue loading the web project.</span></span>
   > 
   > 
5. <span data-ttu-id="8f954-166">**정보** 페이지로 가서 응용 프로그램이 **Azure Table Storage** 리포지토리를 사용하고 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="8f954-166">Browse to the **About** page to verify that the application is using the **Azure Table Storage** repository.</span></span>
   
     ![웹 브라우저](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleAzureTableStorageAbout.png)

## <a name="explore-the-azure-table-storage"></a><span data-ttu-id="8f954-168">Azure 테이블 저장소 탐색</span><span class="sxs-lookup"><span data-stu-id="8f954-168">Explore the Azure Table Storage</span></span>
<span data-ttu-id="8f954-169">Visual Studio에서 클라우드 탐색기를 사용하여 저장소 테이블을 쉽게 보고 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f954-169">It's easy to view and edit storage tables using Cloud Explorer in Visual Studio.</span></span> <span data-ttu-id="8f954-170">이 섹션에서는 서버 탐색기를 사용하여 설문 조사 응용 프로그램 테이블의 내용을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="8f954-170">In this section we'll use Server Explorer to view the contents of the polls application tables.</span></span>

> [!NOTE]
> <span data-ttu-id="8f954-171">이를 위해서는 [Azure SDK for .NET]의 일부로 사용할 수 있는 Microsoft Azure 도구가 설치되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f954-171">This requires Microsoft Azure Tools to be installed, which are available as part of the [Azure SDK for .NET].</span></span>
> 
> 

1. <span data-ttu-id="8f954-172">**클라우드 탐색기**를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="8f954-172">Open **Cloud Explorer**.</span></span> <span data-ttu-id="8f954-173">**저장소 계정**, 사용자의 저장소 계정 및 **테이블**을 차례로 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="8f954-173">Expand **Storage Accounts**, your storage account, then **Tables**.</span></span>
   
     ![클라우드 탐색기](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonServerExplorer.png)
2. <span data-ttu-id="8f954-175">**polls** 또는 **choices** 테이블을 두 번 클릭하여 문서 창에서 테이블 내용을 확인하고 add/remove/edit 엔터티를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f954-175">Double-click on the **polls** or **choices** table to view the contents of the table in a document window, as well as add/remove/edit entities.</span></span>
   
     ![테이블 쿼리 결과](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonServerExplorerTable.png)

## <a name="publish-the-web-app-to-azure-app-service"></a><span data-ttu-id="8f954-177">Azure 앱 서비스에 웹앱 게시</span><span class="sxs-lookup"><span data-stu-id="8f954-177">Publish the web app to Azure App Service</span></span>
<span data-ttu-id="8f954-178">Azure .NET SDK를 통해 Azure 앱 서비스에 웹앱을 쉽게 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f954-178">The Azure .NET SDK provides an easy way to deploy your web app to Azure App Service.</span></span>

1. <span data-ttu-id="8f954-179">**솔루션 탐색기**에서 프로젝트 노드를 마우스 오른쪽 단추로 클릭하고 **게시**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8f954-179">In **Solution Explorer**, right-click on the project node and select **Publish**.</span></span>
   
     ![웹 게시 대화 상자](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonPublishWebSiteDialog.png)
2. <span data-ttu-id="8f954-181">**Microsoft Azure 웹앱**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8f954-181">Click on **Microsoft Azure Web Apps**.</span></span>
3. <span data-ttu-id="8f954-182">**새로 만들기** 를 클릭하여 새 웹앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8f954-182">Click on **New** to create a new web app.</span></span>
4. <span data-ttu-id="8f954-183">다음 필드에 입력하고 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8f954-183">Fill in the following fields and click **Create**.</span></span>
   
   * <span data-ttu-id="8f954-184">**웹앱 이름**</span><span class="sxs-lookup"><span data-stu-id="8f954-184">**Web App name**</span></span>
   * <span data-ttu-id="8f954-185">**앱 서비스 계획**</span><span class="sxs-lookup"><span data-stu-id="8f954-185">**App Service plan**</span></span>
   * <span data-ttu-id="8f954-186">**리소스 그룹**</span><span class="sxs-lookup"><span data-stu-id="8f954-186">**Resource group**</span></span>
   * <span data-ttu-id="8f954-187">**지역**</span><span class="sxs-lookup"><span data-stu-id="8f954-187">**Region**</span></span>
   * <span data-ttu-id="8f954-188">**데이터베이스 서버**를 **데이터베이스 없음**으로 그대로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="8f954-188">Leave **Database server** set to **No database**</span></span>
5. <span data-ttu-id="8f954-189">다른 모든 기본값을 그대로 적용하고 **게시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8f954-189">Accept all other defaults and click **Publish**.</span></span>
6. <span data-ttu-id="8f954-190">웹 브라우저가 자동으로 게시된 웹앱으로 열립니다.</span><span class="sxs-lookup"><span data-stu-id="8f954-190">Your web browser will open automatically to the published web app.</span></span> <span data-ttu-id="8f954-191">정보 페이지로 이동하면 **Azure Table Storage** 리포지토리가 아니라 **메모리 내** 리포지토리를 사용한다는 것을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f954-191">If you browse to the about page, you'll see that it uses the **In-Memory** repository, not the **Azure Table Storage** repository.</span></span>
   
   <span data-ttu-id="8f954-192">환경 변수가 Azure 앱 서비스의 웹앱 인스턴스에 설정되어 있지 않아서 **settings.py**에 지정된 기본값을 사용하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="8f954-192">That's because the environment variables are not set on the Web Apps instance in Azure App Service, so it uses the default values specified in **settings.py**.</span></span>

## <a name="configure-the-web-apps-instance"></a><span data-ttu-id="8f954-193">웹앱 인스턴스 구성</span><span class="sxs-lookup"><span data-stu-id="8f954-193">Configure the Web Apps instance</span></span>
<span data-ttu-id="8f954-194">이 섹션에서는 웹앱 인스턴스에 대한 환경 변수를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="8f954-194">In this section, we'll configure environment variables for the Web Apps instance.</span></span>

1. <span data-ttu-id="8f954-195">[Azure Portal]에서 **찾아보기** > **App Services** > 사용자의 웹앱 이름을 클릭하여 웹앱 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="8f954-195">In [Azure Portal], open the web app's blade by clicking **Browse** > **App Services** > your web app name.</span></span>
2. <span data-ttu-id="8f954-196">웹앱 블레이드에서 **모든 설정**을 클릭한 다음 **응용 프로그램 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8f954-196">In your web app's blade, click **All Settings**, then click **Application Settings**.</span></span>
3. <span data-ttu-id="8f954-197">**앱 설정** 섹션으로 스크롤한 후 위의 **프로젝트 구성** 섹션에 설명된 대로 **REPOSITORY\_NAME**, **STORAGE\_NAME** 및 **STORAGE\_KEY** 값을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="8f954-197">Scroll down to the **App settings** section and set the values for **REPOSITORY\_NAME**, **STORAGE\_NAME** and **STORAGE\_KEY** as described in the **Configure the project** section above.</span></span>
   
     ![앱 설정](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonWebSiteConfigureSettingsTableStorage.png)
4. <span data-ttu-id="8f954-199">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8f954-199">Click on **Save**.</span></span> <span data-ttu-id="8f954-200">변경 내용이 적용되었다는 알림을 받은 후에 웹앱 주 블레이드에서 **찾아보기** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8f954-200">After you've received the notifications that the changes were applied, click on **Browse** from the Web app main blade.</span></span>
5. <span data-ttu-id="8f954-201">**Azure 테이블 저장소** 리포지토리를 사용하여 예상한 대로 웹앱이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="8f954-201">You should see the web app working as expected, using the **Azure Table Storage** repository.</span></span>
   
   <span data-ttu-id="8f954-202">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="8f954-202">Congratulations!</span></span>
   
     ![웹 브라우저](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleAzureBrowser.png)

## <a name="next-steps"></a><span data-ttu-id="8f954-204">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8f954-204">Next steps</span></span>
<span data-ttu-id="8f954-205">Python Tools for Visual Studio, Bottle 및 Azure 테이블 저장소에 대해 자세히 알아보려면 다음 링크를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8f954-205">Follow these links to learn more about Python Tools for Visual Studio, Bottle and Azure Table Storage.</span></span>

* <span data-ttu-id="8f954-206">[Python Tools for Visual Studio 설명서]</span><span class="sxs-lookup"><span data-stu-id="8f954-206">[Python Tools for Visual Studio Documentation]</span></span>
  * <span data-ttu-id="8f954-207">[웹 프로젝트]</span><span class="sxs-lookup"><span data-stu-id="8f954-207">[Web Projects]</span></span>
  * <span data-ttu-id="8f954-208">[클라우드 서비스 프로젝트]</span><span class="sxs-lookup"><span data-stu-id="8f954-208">[Cloud Service Projects]</span></span>
  * <span data-ttu-id="8f954-209">[Microsoft Azure의 원격 디버깅]</span><span class="sxs-lookup"><span data-stu-id="8f954-209">[Remote Debugging on Microsoft Azure]</span></span>
* <span data-ttu-id="8f954-210">[Bottle 설명서]</span><span class="sxs-lookup"><span data-stu-id="8f954-210">[Bottle Documentation]</span></span>
* <span data-ttu-id="8f954-211">[Azure 저장소]</span><span class="sxs-lookup"><span data-stu-id="8f954-211">[Azure Storage]</span></span>
* <span data-ttu-id="8f954-212">[Python용 Azure SDK]</span><span class="sxs-lookup"><span data-stu-id="8f954-212">[Azure SDK for Python]</span></span>
* <span data-ttu-id="8f954-213">[Python에서 테이블 저장소 서비스를 사용하는 방법]</span><span class="sxs-lookup"><span data-stu-id="8f954-213">[How to Use the Table Storage Service from Python]</span></span>

## <a name="whats-changed"></a><span data-ttu-id="8f954-214">변경된 내용</span><span class="sxs-lookup"><span data-stu-id="8f954-214">What's changed</span></span>
* <span data-ttu-id="8f954-215">웹 사이트에서 앱 서비스로의 변경에 대한 지침은 [Azure 앱 서비스와 이 서비스가 기존 Azure 서비스에 미치는 영향](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="8f954-215">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!--Link references-->
[Python 개발자 센터]: /develop/python/
[Azure 클라우드 서비스]: ../cloud-services/cloud-services-python-ptvs.md
[설명서]:../cosmos-db/table-storage-how-to-use-python.md
[Python에서 테이블 저장소 서비스를 사용하는 방법]:../cosmos-db/table-storage-how-to-use-python.md


<!--External Link references-->
[Azure Portal]: https://portal.azure.com
[Azure SDK for .NET]: http://azure.microsoft.com/downloads/
[Python Tools for Visual Studio]: http://aka.ms/ptvs
[Python Tools 2.2 for Visual Studio]: http://go.microsoft.com/fwlink/?LinkId=624025
[Python Tools 2.2 for Visual Studio Samples VSIX]: http://go.microsoft.com/fwlink/?LinkId=624025
[Azure SDK Tools for VS 2015]: http://go.microsoft.com/fwlink/?LinkId=518003
[Python 2.7 32비트]: http://go.microsoft.com/fwlink/?LinkId=517190
[Python 3.4 32비트]: http://go.microsoft.com/fwlink/?LinkId=517191
[Python Tools for Visual Studio 설명서]: http://aka.ms/ptvsdocs
[Bottle 설명서]: http://bottlepy.org/docs/dev/index.html
[Microsoft Azure의 원격 디버깅]: http://go.microsoft.com/fwlink/?LinkId=624026
[웹 프로젝트]: http://go.microsoft.com/fwlink/?LinkId=624027
[클라우드 서비스 프로젝트]: http://go.microsoft.com/fwlink/?LinkId=624028
[Azure 저장소]: http://azure.microsoft.com/documentation/services/storage/
[Python용 Azure SDK]: https://github.com/Azure/azure-sdk-for-python
