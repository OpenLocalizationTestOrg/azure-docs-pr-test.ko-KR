---
title: "aaaBottle 및 Python Tools 2.2 for Visual Studio를 사용 하 여 Azure에서 Azure 테이블 저장소"
description: "어떻게 toouse hello Python Tools toocreate Visual Studio에 대 한 Azure 테이블 저장소에 데이터를 저장 하는 Bottle 응용 프로그램 학습과 hello 웹 응용 프로그램 tooAzure 앱 서비스 웹 앱을 배포 합니다."
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
ms.openlocfilehash: 25b9eb002b8748483d5b9458b7b5860a958b4bb3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="bottle-and-azure-table-storage-on-azure-with-python-tools-22-for-visual-studio"></a><span data-ttu-id="a15a2-103">Azure의 Bottle 및 Azure 테이블 저장소와 Python Tools 2.2 for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a15a2-103">Bottle and Azure Table Storage on Azure with Python Tools 2.2 for Visual Studio</span></span>
<span data-ttu-id="a15a2-104">이 자습서에서는 [Python Tools for Visual Studio] toocreate 단순 hello PTVS 샘플 템플릿 중 하나를 사용 하 여 웹 앱을 폴링합니다.</span><span class="sxs-lookup"><span data-stu-id="a15a2-104">In this tutorial, we'll use [Python Tools for Visual Studio] toocreate a simple polls web app using one of hello PTVS sample templates.</span></span> <span data-ttu-id="a15a2-105">이 자습서는 [비디오](https://www.youtube.com/watch?v=GJXDGaEPy94)로도 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="a15a2-105">This tutorial is also available as a [video](https://www.youtube.com/watch?v=GJXDGaEPy94).</span></span>

<span data-ttu-id="a15a2-106">hello 설문 웹 응용 프로그램 저장소 (메모리 내에서 Azure 테이블 저장소 MongoDB)의 서로 다른 유형을 쉽게 전환할 수 있도록 해당 저장소에 대 한 추상화를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="a15a2-106">hello polls web app defines an abstraction for its repository, so you can easily switch between different types of repositories (In-Memory, Azure Table Storage, MongoDB).</span></span>

<span data-ttu-id="a15a2-107">어떻게 toocreate Azure 저장소 계정, tooconfigure hello 웹 앱 toouse Azure 테이블 저장소, 방법 등에 대해 배워 봅니다 우리 toopublish 웹 앱이 너무 hello[Azure 앱 서비스 웹 앱](http://go.microsoft.com/fwlink/?LinkId=529714)합니다.</span><span class="sxs-lookup"><span data-stu-id="a15a2-107">We'll learn how toocreate an Azure Storage account, how tooconfigure hello web app toouse Azure Table Storage, and how toopublish hello web app too[Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

<span data-ttu-id="a15a2-108">Hello 참조 [Python 개발자 센터] Bottle를 사용 하 여 ptvs Azure 앱 서비스 웹 앱의 개발을 설명 하는 다른 문서 플라스 및 Django 웹 프레임 워크, MongoDB, Azure 테이블 저장소, MySQL 및 SQL 데이터베이스 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="a15a2-108">See hello [Python Developer Center] for more articles that cover development of Azure App Service Web Apps with PTVS using Bottle, Flask and Django web frameworks, with MongoDB, Azure Table Storage, MySQL and SQL Database services.</span></span> <span data-ttu-id="a15a2-109">개발 하는 경우 hello 단계는 유사 하지만이 문서에서는 앱 서비스, [Azure 클라우드 서비스]합니다.</span><span class="sxs-lookup"><span data-stu-id="a15a2-109">While this article focuses on App Service, hello steps are similar when developing [Azure Cloud Services].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a15a2-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="a15a2-110">Prerequisites</span></span>
* <span data-ttu-id="a15a2-111">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="a15a2-111">Visual Studio 2015</span></span>
* <span data-ttu-id="a15a2-112">[Python Tools 2.2 for Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="a15a2-112">[Python Tools 2.2 for Visual Studio]</span></span>
* <span data-ttu-id="a15a2-113">[VSIX Visual Studio 샘플에 대 한 Python Tools 2.2]</span><span class="sxs-lookup"><span data-stu-id="a15a2-113">[Python Tools 2.2 for Visual Studio Samples VSIX]</span></span>
* <span data-ttu-id="a15a2-114">[Azure SDK Tools for VS 2015]</span><span class="sxs-lookup"><span data-stu-id="a15a2-114">[Azure SDK Tools for VS 2015]</span></span>
* <span data-ttu-id="a15a2-115">[Python 2.7 32비트] 또는 [Python 3.4 32비트]</span><span class="sxs-lookup"><span data-stu-id="a15a2-115">[Python 2.7 32-bit] or [Python 3.4 32-bit]</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="a15a2-116">Tooget Azure 계정에 등록 하기 전에 Azure 앱 서비스를 시작 하려는 경우 너무 이동[앱 서비스 시도](https://azure.microsoft.com/try/app-service/)앱 서비스의 수명이 짧은 스타터 웹 응용 프로그램 즉시 만들 수 있는, 합니다.</span><span class="sxs-lookup"><span data-stu-id="a15a2-116">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="a15a2-117">신용 카드는 필요하지 않으며 약정도 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a15a2-117">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="create-hello-project"></a><span data-ttu-id="a15a2-118">Hello 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="a15a2-118">Create hello Project</span></span>
<span data-ttu-id="a15a2-119">이 섹션에서는 샘플 템플릿을 사용하여 Visual Studio 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a15a2-119">In this section, we'll create a Visual Studio project using a sample template.</span></span> <span data-ttu-id="a15a2-120">가상 환경을 만들고 필요한 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="a15a2-120">We'll create a virtual environment and install required packages.</span></span> <span data-ttu-id="a15a2-121">다음 hello 기본 메모리 저장소를 사용 하 여 로컬로 hello 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a15a2-121">Then we'll run hello application locally using hello default in-memory repository.</span></span>

1. <span data-ttu-id="a15a2-122">Visual Studio에서 **파일**, **새 프로젝트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a15a2-122">In Visual Studio, select **File**, **New Project**.</span></span>
2. <span data-ttu-id="a15a2-123">프로젝트 템플릿 hello에서 hello [VSIX Visual Studio 샘플에 대 한 Python Tools 2.2] 아래에서 사용할 수 있는 **Python**, **샘플**합니다.</span><span class="sxs-lookup"><span data-stu-id="a15a2-123">hello project templates from hello [Python Tools 2.2 for Visual Studio Samples VSIX] are available under **Python**, **Samples**.</span></span> <span data-ttu-id="a15a2-124">선택 **설문 Bottle 웹 프로젝트** 확인 toocreate hello 프로젝트를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="a15a2-124">Select **Polls Bottle Web Project** and click OK toocreate hello project.</span></span>
   
     ![새 프로젝트 대화 상자](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleNewProject.png)
3. <span data-ttu-id="a15a2-126">외부 패키지 입력 정보 요청된 tooinstall 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a15a2-126">You will be prompted tooinstall external packages.</span></span> <span data-ttu-id="a15a2-127">**가상 환경에 설치**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a15a2-127">Select **Install into a virtual environment**.</span></span>
   
     ![외부 패키지 대화 상자](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleExternalPackages.png)
4. <span data-ttu-id="a15a2-129">선택 **Python 2.7** 또는 **Python 3.4** hello 기본 해석기로 합니다.</span><span class="sxs-lookup"><span data-stu-id="a15a2-129">Select **Python 2.7** or **Python 3.4** as hello base interpreter.</span></span>
   
     ![가상 환경 추가 대화 상자](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonAddVirtualEnv.png)
5. <span data-ttu-id="a15a2-131">Hello 응용 프로그램 키를 눌러 작동 하는지 확인 `F5`합니다.</span><span class="sxs-lookup"><span data-stu-id="a15a2-131">Confirm that hello application works by pressing `F5`.</span></span> <span data-ttu-id="a15a2-132">기본적으로 hello 응용 프로그램에는 구성이 필요 하지 않습니다는 메모리 내 저장소를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a15a2-132">By default, hello application uses an in-memory repository which doesn't require any configuration.</span></span> <span data-ttu-id="a15a2-133">Hello 웹 서버를 중지 하는 경우 모든 데이터가 손실 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a15a2-133">All data is lost when hello web server is stopped.</span></span>
6. <span data-ttu-id="a15a2-134">**Create Sample Polls**를 클릭하고 poll and vote를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a15a2-134">Click **Create Sample Polls**, then click on a poll and vote.</span></span>
   
     ![웹 브라우저](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleInMemoryBrowser.png)

## <a name="create-an-azure-storage-account"></a><span data-ttu-id="a15a2-136">Azure 저장소 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="a15a2-136">Create an Azure Storage Account</span></span>
<span data-ttu-id="a15a2-137">toouse 저장소 작업을 Azure 저장소 계정이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="a15a2-137">toouse storage operations, you need an Azure storage account.</span></span> <span data-ttu-id="a15a2-138">다음 단계에 따라 저장소 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a15a2-138">You can create a storage account by following these steps.</span></span>

1. <span data-ttu-id="a15a2-139">Hello에 로그인 [Azure 포털](https://portal.azure.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="a15a2-139">Log into hello [Azure Portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="a15a2-140">Hello 클릭 **새로** hello 위에 표시 아이콘 hello 포털의 왼쪽을 클릭 한 다음 **데이터 + 저장소** > **저장소 계정**합니다.</span><span class="sxs-lookup"><span data-stu-id="a15a2-140">Click hello **New** icon on hello top left of hello Portal, then click **Data + Storage** > **Storage Account**.</span></span>  <span data-ttu-id="a15a2-141">Hello 클릭 **만들기** 단추 hello 저장소 계정에 고유한 이름을 지정 하 고 새 [리소스 그룹](../azure-resource-manager/resource-group-overview.md) 것에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="a15a2-141">Click hello **Create** button, then give hello storage account a unique name and create a new [resource group](../azure-resource-manager/resource-group-overview.md) for it.</span></span>
   
      ![빠른 생성](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonAzureStorageCreate.png)
   
    <span data-ttu-id="a15a2-143">Hello 저장소 계정이 생성 되 면 hello **알림** 단추가 녹색 깜박입니다 **성공** 블레이드 hello 저장소 계정을 열릴 및 tooshow 속하는지 toohello 새 리소스 그룹 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="a15a2-143">When hello storage account has been created, hello **Notifications** button will flash a green **SUCCESS** and hello storage account's blade is open tooshow that it belongs toohello new resource group you created.</span></span>
3. <span data-ttu-id="a15a2-144">Hello 클릭 **선택키가** hello 저장소 계정의 블레이드에서 부분입니다.</span><span class="sxs-lookup"><span data-stu-id="a15a2-144">Click hello **Access keys** part in hello storage account's blade.</span></span> <span data-ttu-id="a15a2-145">Hello 계정 이름 및 key1 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="a15a2-145">Take note of hello account name and key1.</span></span>
   
      ![구성](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonAzureStorageKeys.png)
   
    <span data-ttu-id="a15a2-147">이 정보 tooconfigure hello 다음 단원의 프로젝트가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="a15a2-147">We will need this information tooconfigure your project in hello next section.</span></span>

## <a name="configure-hello-project"></a><span data-ttu-id="a15a2-148">Hello 프로젝트 구성</span><span class="sxs-lookup"><span data-stu-id="a15a2-148">Configure hello Project</span></span>
<span data-ttu-id="a15a2-149">이 섹션에서는 방금 만든 응용 프로그램 toouse hello 저장소 계좌를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="a15a2-149">In this section, we'll configure our application toouse hello storage account we just created.</span></span> <span data-ttu-id="a15a2-150">다음 로컬로 hello 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a15a2-150">Then we'll run hello application locally.</span></span>

1. <span data-ttu-id="a15a2-151">Visual Studio의 솔루션 탐색기에서 프로젝트 노드를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a15a2-151">In Visual Studio, right-click on your project node in Solution Explorer and select **Properties**.</span></span> <span data-ttu-id="a15a2-152">Hello 클릭 **디버그** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="a15a2-152">Click on hello **Debug** tab.</span></span>
   
     ![프로젝트 디버그 설정](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleAzureTableStorageProjectDebugSettings.png)
2. <span data-ttu-id="a15a2-154">Hello에 hello 응용 프로그램에서 요구 하는 환경 변수 값 설정 **서버 명령은 디버그**, **환경**합니다.</span><span class="sxs-lookup"><span data-stu-id="a15a2-154">Set hello values of environment variables required by hello application in **Debug Server Command**, **Environment**.</span></span>
   
       REPOSITORY_NAME=azuretablestorage
       STORAGE_NAME=<storage account name>
       STORAGE_KEY=<primary access key>
   
   <span data-ttu-id="a15a2-155">이렇게 하면 hello 환경 변수 설정 됩니다 때 있습니다 **디버깅 시작**합니다.</span><span class="sxs-lookup"><span data-stu-id="a15a2-155">This will set hello environment variables when you **Start Debugging**.</span></span> <span data-ttu-id="a15a2-156">Hello 변수 toobe 경우에 설정 하려는 경우 있습니다 **디버깅 하지 않고 시작**, 아래 값을 동일한 집합 hello **서버 명령 실행** 도 합니다.</span><span class="sxs-lookup"><span data-stu-id="a15a2-156">If you want hello variables toobe set when you **Start Without Debugging**, set hello same values under **Run Server Command** as well.</span></span>
   
   <span data-ttu-id="a15a2-157">또는 Windows 제어판 hello를 사용 하 여 환경 변수를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a15a2-157">Alternatively, you can define environment variables using hello Windows Control Panel.</span></span> <span data-ttu-id="a15a2-158">프로젝트 파일 / 원하는 tooavoid 소스 코드에서 자격 증명을 저장 하는 경우 더 나은 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="a15a2-158">This is a better option if you want tooavoid storing credentials in source code / project file.</span></span> <span data-ttu-id="a15a2-159">값은 toobe toohello 사용할 수 있는 응용 프로그램 참고 hello 새 환경에 대 한 toorestart Visual Studio가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="a15a2-159">Note that you will need toorestart Visual Studio for hello new environment values toobe available toohello application.</span></span>
3. <span data-ttu-id="a15a2-160">hello Azure 테이블 저장소 리포지토리를 구현 하는 hello 코드는 **models/azuretablestorage.py**합니다.</span><span class="sxs-lookup"><span data-stu-id="a15a2-160">hello code that implements hello Azure Table Storage repository is in **models/azuretablestorage.py**.</span></span> <span data-ttu-id="a15a2-161">Hello 참조 [설명서] 방법에 대 한 자세한 내용은 toouse Python에서 테이블 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="a15a2-161">See hello [documentation] for more information on how toouse Table Service from Python.</span></span>
4. <span data-ttu-id="a15a2-162">Hello 응용 프로그램을 실행 `F5`합니다.</span><span class="sxs-lookup"><span data-stu-id="a15a2-162">Run hello application with `F5`.</span></span> <span data-ttu-id="a15a2-163">사용 하 여 만든 설문 **샘플 설문 만들** 투표 제출한 hello 데이터는 Azure 테이블 저장소에 serialize 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a15a2-163">Polls that are created with **Create Sample Polls** and hello data submitted by voting will be serialized in Azure Table Storage.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="a15a2-164">hello Python 2.7 가상 환경에는 Visual Studio에서 예외 나누기가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a15a2-164">hello Python 2.7 Virtual Environment may cause an exception break in Visual Studio.</span></span>  <span data-ttu-id="a15a2-165">키를 눌러 `F5` toocontinue hello 웹 프로젝트를 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="a15a2-165">Press `F5` toocontinue loading hello web project.</span></span>
   > 
   > 
5. <span data-ttu-id="a15a2-166">Toohello 찾아보기 **에 대 한** hello 응용 프로그램 페이지 tooverify hello를 사용 하는 **Azure 테이블 저장소** 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="a15a2-166">Browse toohello **About** page tooverify that hello application is using hello **Azure Table Storage** repository.</span></span>
   
     ![웹 브라우저](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleAzureTableStorageAbout.png)

## <a name="explore-hello-azure-table-storage"></a><span data-ttu-id="a15a2-168">Hello Azure 테이블 저장소를 탐색 합니다.</span><span class="sxs-lookup"><span data-stu-id="a15a2-168">Explore hello Azure Table Storage</span></span>
<span data-ttu-id="a15a2-169">쉽게 tooview 이며 클라우드 탐색기를 사용 하 여 Visual Studio에서 저장소 테이블을 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="a15a2-169">It's easy tooview and edit storage tables using Cloud Explorer in Visual Studio.</span></span> <span data-ttu-id="a15a2-170">이 섹션의 hello 여론 조사 응용 프로그램 테이블 내용의 tooview hello 서버 탐색기를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a15a2-170">In this section we'll use Server Explorer tooview hello contents of hello polls application tables.</span></span>

> [!NOTE]
> <span data-ttu-id="a15a2-171">사용할 수는 설치 된 Microsoft Azure 도구 toobe이 필요 hello의 일부로 [Azure SDK for.NET]합니다.</span><span class="sxs-lookup"><span data-stu-id="a15a2-171">This requires Microsoft Azure Tools toobe installed, which are available as part of hello [Azure SDK for .NET].</span></span>
> 
> 

1. <span data-ttu-id="a15a2-172">**클라우드 탐색기**를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="a15a2-172">Open **Cloud Explorer**.</span></span> <span data-ttu-id="a15a2-173">**저장소 계정**, 사용자의 저장소 계정 및 **테이블**을 차례로 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="a15a2-173">Expand **Storage Accounts**, your storage account, then **Tables**.</span></span>
   
     ![Cloud Explorer](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonServerExplorer.png)
2. <span data-ttu-id="a15a2-175">Hello에 두 번 클릭 **설문** 또는 **선택** tooview hello 내용의 hello 테이블 추가/제거/편집 엔터티를 비롯 하 여 문서 창에 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="a15a2-175">Double-click on hello **polls** or **choices** table tooview hello contents of hello table in a document window, as well as add/remove/edit entities.</span></span>
   
     ![테이블 쿼리 결과](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonServerExplorerTable.png)

## <a name="publish-hello-web-app-tooazure-app-service"></a><span data-ttu-id="a15a2-177">Hello 웹 응용 프로그램 tooAzure 앱 서비스를 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="a15a2-177">Publish hello web app tooAzure App Service</span></span>
<span data-ttu-id="a15a2-178">Azure.NET SDK hello 쉽게 toodeploy 웹 앱 tooAzure 앱 서비스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a15a2-178">hello Azure .NET SDK provides an easy way toodeploy your web app tooAzure App Service.</span></span>

1. <span data-ttu-id="a15a2-179">**솔루션 탐색기**hello 프로젝트 노드를 마우스 오른쪽 단추로 클릭 하 고 선택 **게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="a15a2-179">In **Solution Explorer**, right-click on hello project node and select **Publish**.</span></span>
   
     ![웹 게시 대화 상자](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonPublishWebSiteDialog.png)
2. <span data-ttu-id="a15a2-181">**Microsoft Azure 웹앱**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a15a2-181">Click on **Microsoft Azure Web Apps**.</span></span>
3. <span data-ttu-id="a15a2-182">클릭 **새로** toocreate 새 웹 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="a15a2-182">Click on **New** toocreate a new web app.</span></span>
4. <span data-ttu-id="a15a2-183">Hello 필드 뒤에 입력 하 고 클릭 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="a15a2-183">Fill in hello following fields and click **Create**.</span></span>
   
   * <span data-ttu-id="a15a2-184">**웹앱 이름**</span><span class="sxs-lookup"><span data-stu-id="a15a2-184">**Web App name**</span></span>
   * <span data-ttu-id="a15a2-185">**앱 서비스 계획**</span><span class="sxs-lookup"><span data-stu-id="a15a2-185">**App Service plan**</span></span>
   * <span data-ttu-id="a15a2-186">**리소스 그룹**</span><span class="sxs-lookup"><span data-stu-id="a15a2-186">**Resource group**</span></span>
   * <span data-ttu-id="a15a2-187">**지역**</span><span class="sxs-lookup"><span data-stu-id="a15a2-187">**Region**</span></span>
   * <span data-ttu-id="a15a2-188">둡니다 **데이터베이스 서버** 도**데이터베이스가 없습니다.**</span><span class="sxs-lookup"><span data-stu-id="a15a2-188">Leave **Database server** set too**No database**</span></span>
5. <span data-ttu-id="a15a2-189">다른 모든 기본값을 그대로 적용하고 **게시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a15a2-189">Accept all other defaults and click **Publish**.</span></span>
6. <span data-ttu-id="a15a2-190">웹 브라우저가 toohello 게시 된 웹 응용 프로그램을 자동으로 열립니다.</span><span class="sxs-lookup"><span data-stu-id="a15a2-190">Your web browser will open automatically toohello published web app.</span></span> <span data-ttu-id="a15a2-191">Hello를 사용 하 여 참조 페이지에 대 한 toohello을 찾아볼 때 **메모리** 저장소, 하지 hello **Azure 테이블 저장소** 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="a15a2-191">If you browse toohello about page, you'll see that it uses hello **In-Memory** repository, not hello **Azure Table Storage** repository.</span></span>
   
   <span data-ttu-id="a15a2-192">hello 환경 변수는 설정 되어 있지 않으므로 Azure 앱 서비스의 웹 앱 인스턴스에 hello에 지정 된 hello 기본값을 사용 하므로 **settings.py**합니다.</span><span class="sxs-lookup"><span data-stu-id="a15a2-192">That's because hello environment variables are not set on hello Web Apps instance in Azure App Service, so it uses hello default values specified in **settings.py**.</span></span>

## <a name="configure-hello-web-apps-instance"></a><span data-ttu-id="a15a2-193">Hello 웹 응용 프로그램 인스턴스 구성</span><span class="sxs-lookup"><span data-stu-id="a15a2-193">Configure hello Web Apps instance</span></span>
<span data-ttu-id="a15a2-194">이 섹션에서는 hello 웹 앱 인스턴스에 대 한 환경 변수를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="a15a2-194">In this section, we'll configure environment variables for hello Web Apps instance.</span></span>

1. <span data-ttu-id="a15a2-195">[Azure 포털], 클릭 하 여 hello 웹 앱 블레이드를 열고 **찾아보기** > **응용 프로그램 서비스** > 웹 응용 프로그램 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="a15a2-195">In [Azure Portal], open hello web app's blade by clicking **Browse** > **App Services** > your web app name.</span></span>
2. <span data-ttu-id="a15a2-196">웹앱 블레이드에서 **모든 설정**을 클릭한 다음 **응용 프로그램 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a15a2-196">In your web app's blade, click **All Settings**, then click **Application Settings**.</span></span>
3. <span data-ttu-id="a15a2-197">Toohello 아래로 스크롤하여 **앱 설정** 섹션 및 설정에 대 한 hello 값 **리포지토리\_이름**, **저장소\_이름** 및  **저장소\_키** hello에 설명 된 대로 **구성 hello 프로젝트** 위의 섹션.</span><span class="sxs-lookup"><span data-stu-id="a15a2-197">Scroll down toohello **App settings** section and set hello values for **REPOSITORY\_NAME**, **STORAGE\_NAME** and **STORAGE\_KEY** as described in hello **Configure hello project** section above.</span></span>
   
     ![앱 설정](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonWebSiteConfigureSettingsTableStorage.png)
4. <span data-ttu-id="a15a2-199">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a15a2-199">Click on **Save**.</span></span> <span data-ttu-id="a15a2-200">Hello 변경 내용이 적용 된 hello 알림을 받은 후 클릭 **찾아보기** hello 웹 앱 블레이드에서 주입니다.</span><span class="sxs-lookup"><span data-stu-id="a15a2-200">After you've received hello notifications that hello changes were applied, click on **Browse** from hello Web app main blade.</span></span>
5. <span data-ttu-id="a15a2-201">Hello를 사용 하 여 예상 대로 hello 웹 응용 프로그램 작업을 참조 해야 **Azure 테이블 저장소** 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="a15a2-201">You should see hello web app working as expected, using hello **Azure Table Storage** repository.</span></span>
   
   <span data-ttu-id="a15a2-202">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="a15a2-202">Congratulations!</span></span>
   
     ![웹 브라우저](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleAzureBrowser.png)

## <a name="next-steps"></a><span data-ttu-id="a15a2-204">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a15a2-204">Next steps</span></span>
<span data-ttu-id="a15a2-205">Visual Studio, Bottle 및 Azure 테이블 저장소에 대 한 Python Tools에 대 한 자세한 이러한 링크 toolearn를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="a15a2-205">Follow these links toolearn more about Python Tools for Visual Studio, Bottle and Azure Table Storage.</span></span>

* <span data-ttu-id="a15a2-206">[Python Tools for Visual Studio 설명서]</span><span class="sxs-lookup"><span data-stu-id="a15a2-206">[Python Tools for Visual Studio Documentation]</span></span>
  * <span data-ttu-id="a15a2-207">[웹 프로젝트]</span><span class="sxs-lookup"><span data-stu-id="a15a2-207">[Web Projects]</span></span>
  * <span data-ttu-id="a15a2-208">[클라우드 서비스 프로젝트]</span><span class="sxs-lookup"><span data-stu-id="a15a2-208">[Cloud Service Projects]</span></span>
  * <span data-ttu-id="a15a2-209">[Microsoft Azure의 원격 디버깅]</span><span class="sxs-lookup"><span data-stu-id="a15a2-209">[Remote Debugging on Microsoft Azure]</span></span>
* <span data-ttu-id="a15a2-210">[Bottle 설명서]</span><span class="sxs-lookup"><span data-stu-id="a15a2-210">[Bottle Documentation]</span></span>
* <span data-ttu-id="a15a2-211">[Azure 저장소]</span><span class="sxs-lookup"><span data-stu-id="a15a2-211">[Azure Storage]</span></span>
* <span data-ttu-id="a15a2-212">[Python용 Azure SDK]</span><span class="sxs-lookup"><span data-stu-id="a15a2-212">[Azure SDK for Python]</span></span>
* <span data-ttu-id="a15a2-213">[어떻게 tooUse hello Python에서 테이블 저장소 서비스]</span><span class="sxs-lookup"><span data-stu-id="a15a2-213">[How tooUse hello Table Storage Service from Python]</span></span>

## <a name="whats-changed"></a><span data-ttu-id="a15a2-214">변경된 내용</span><span class="sxs-lookup"><span data-stu-id="a15a2-214">What's changed</span></span>
* <span data-ttu-id="a15a2-215">웹 사이트 tooApp 서비스에서에서 변경 사항 참조 가이드 toohello: [기존 Azure 서비스에 대 한 해당 영향 및 Azure 앱 서비스](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="a15a2-215">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!--Link references-->
[Python 개발자 센터]: /develop/python/
[Azure 클라우드 서비스]: ../cloud-services/cloud-services-python-ptvs.md
[설명서]:../cosmos-db/table-storage-how-to-use-python.md
[어떻게 tooUse hello Python에서 테이블 저장소 서비스]:../cosmos-db/table-storage-how-to-use-python.md


<!--External Link references-->
[Azure 포털]: https://portal.azure.com
[Azure SDK for.NET]: http://azure.microsoft.com/downloads/
[Python Tools for Visual Studio]: http://aka.ms/ptvs
[Python Tools 2.2 for Visual Studio]: http://go.microsoft.com/fwlink/?LinkId=624025
[VSIX Visual Studio 샘플에 대 한 Python Tools 2.2]: http://go.microsoft.com/fwlink/?LinkId=624025
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
