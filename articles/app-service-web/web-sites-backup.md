---
title: "Azure에서 앱을 aaaBack"
description: "자세한 방법을 Azure 앱 서비스에서 앱의 toocreate 백업 합니다."
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: jimbe
ms.assetid: 6223b6bd-84ec-48df-943f-461d84605694
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2016
ms.author: cephalin
ms.openlocfilehash: e41d93d322bbc48b45b28eeaa817928d83c2b9d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-your-app-in-azure"></a><span data-ttu-id="c2c98-103">Azure에서 앱 백업</span><span class="sxs-lookup"><span data-stu-id="c2c98-103">Back up your app in Azure</span></span>
<span data-ttu-id="c2c98-104">hello를 백업 및 복원 기능에 [Azure 앱 서비스](../app-service/app-service-value-prop-what-is.md) 앱 백업을 수동으로 또는 일정에 따라 쉽게 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2c98-104">hello Back up and Restore feature in [Azure App Service](../app-service/app-service-value-prop-what-is.md) lets you easily create app backups manually or on a schedule.</span></span> <span data-ttu-id="c2c98-105">덮어쓰기를 hello 기존 응용 프로그램 또는 tooanother 응용 프로그램을 복원 하 여 hello 앱 tooa 스냅숏을 이전 상태로 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2c98-105">You can restore hello app tooa snapshot of a previous state by overwriting hello existing app or restoring tooanother app.</span></span> 

<span data-ttu-id="c2c98-106">앱을 백업에서 복원하는 방법에 대한 자세한 내용은 [Azure에서 앱 복원](web-sites-restore.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c2c98-106">For information on restoring an app from backup, see [Restore an app in Azure](web-sites-restore.md).</span></span>

<a name="whatsbackedup"></a>

## <a name="what-gets-backed-up"></a><span data-ttu-id="c2c98-107">백업 대상</span><span class="sxs-lookup"><span data-stu-id="c2c98-107">What gets backed up</span></span>
<span data-ttu-id="c2c98-108">앱 서비스는 hello 다음을 백업할 수 정보 tooan Azure 저장소 계정 및 컨테이너 응용 프로그램 toouse를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2c98-108">App Service can backup hello following information tooan Azure storage account and container that you have configured your app toouse.</span></span> 

* <span data-ttu-id="c2c98-109">앱 구성</span><span class="sxs-lookup"><span data-stu-id="c2c98-109">App configuration</span></span>
* <span data-ttu-id="c2c98-110">파일 콘텐츠</span><span class="sxs-lookup"><span data-stu-id="c2c98-110">File content</span></span>
* <span data-ttu-id="c2c98-111">데이터베이스 연결 된 tooyour 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="c2c98-111">Database connected tooyour app</span></span>

<span data-ttu-id="c2c98-112">hello 데이터베이스 솔루션을 다음 백업 기능으로 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c2c98-112">hello following database solutions are supported with backup feature:</span></span> 
   - [<span data-ttu-id="c2c98-113">SQL 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="c2c98-113">SQL Database</span></span>](https://azure.microsoft.com/en-us/services/sql-database/)
   - [<span data-ttu-id="c2c98-114">Azure Database for MySQL(미리 보기)</span><span class="sxs-lookup"><span data-stu-id="c2c98-114">Azure Database for MySQL (Preview)</span></span>](https://azure.microsoft.com/en-us/services/mysql)
   - [<span data-ttu-id="c2c98-115">Azure Database for PostgreSQL(미리 보기)</span><span class="sxs-lookup"><span data-stu-id="c2c98-115">Azure Database for PostgreSQL (Preview)</span></span>](https://azure.microsoft.com/en-us/services/postgres)
   - [<span data-ttu-id="c2c98-116">ClearDB MySQL</span><span class="sxs-lookup"><span data-stu-id="c2c98-116">ClearDB MySQL</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/SuccessBricksInc.ClearDBMySQLDatabase?tab=Overview)
   - [<span data-ttu-id="c2c98-117">MySQL 인앱</span><span class="sxs-lookup"><span data-stu-id="c2c98-117">MySQL in-app</span></span>](https://blogs.msdn.microsoft.com/appserviceteam/2017/03/06/announcing-general-availability-for-mysql-in-app)
 

> [!NOTE]
>  <span data-ttu-id="c2c98-118">각 백업은 증분 업데이트가 아니라 앱의 완전한 오프라인 복사본입니다.</span><span class="sxs-lookup"><span data-stu-id="c2c98-118">Each backup is a complete offline copy of your app, not an incremental update.</span></span>
>  

<a name="requirements"></a>

## <a name="requirements-and-restrictions"></a><span data-ttu-id="c2c98-119">요구 사항 및 제한 사항</span><span class="sxs-lookup"><span data-stu-id="c2c98-119">Requirements and restrictions</span></span>
* <span data-ttu-id="c2c98-120">hello를 백업 및 복원 기능을 사용 하려면 앱 서비스 계획 toobe hello에 hello **표준** 계층 또는 **프리미엄** 계층입니다.</span><span class="sxs-lookup"><span data-stu-id="c2c98-120">hello Back up and Restore feature requires hello App Service plan toobe in hello **Standard** tier or **Premium** tier.</span></span> <span data-ttu-id="c2c98-121">앱 서비스 계획 toouse 더 높은 계층 확장에 대 한 자세한 내용은 참조 [Azure에서 응용 프로그램을 수직](web-sites-scale.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c2c98-121">For more information about scaling your App Service plan toouse a higher tier, see [Scale up an app in Azure](web-sites-scale.md).</span></span>  
  <span data-ttu-id="c2c98-122">**프리미엄** 계층을 사용하면 **표준** 계층보다 더 많은 매일 백업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2c98-122">**Premium** tier allows a greater number of daily back ups than **Standard** tier.</span></span>
* <span data-ttu-id="c2c98-123">Azure 저장소 계정 및 컨테이너에서 hello 필요 toobackup hello 앱과 동일한 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2c98-123">You need an Azure storage account and container in hello same subscription as hello app that you want toobackup.</span></span> <span data-ttu-id="c2c98-124">Azure 저장소 계정에 대 한 자세한 내용은 참조 hello [링크](#moreaboutstorage) hello이이 문서의 뒷부분에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2c98-124">For more information on Azure storage accounts, see hello [links](#moreaboutstorage) at hello end of this article.</span></span>
* <span data-ttu-id="c2c98-125">응용 프로그램 및 데이터베이스 콘텐츠 too10 GB 백업 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2c98-125">Backups can be up too10 GB of app and database content.</span></span> <span data-ttu-id="c2c98-126">Hello 백업 크기가이 한도 초과 하면 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2c98-126">If hello backup size exceeds this limit, you get an error .</span></span>

<a name="manualbackup"></a>

## <a name="create-a-manual-backup"></a><span data-ttu-id="c2c98-127">수동 백업 만들기</span><span class="sxs-lookup"><span data-stu-id="c2c98-127">Create a manual backup</span></span>
1. <span data-ttu-id="c2c98-128">Hello에 [Azure 포털](https://portal.azure.com)tooyour 앱 블레이드를 탐색, 선택, **백업을**합니다.</span><span class="sxs-lookup"><span data-stu-id="c2c98-128">In hello [Azure Portal](https://portal.azure.com), navigate tooyour app's blade, select **Backups**.</span></span> <span data-ttu-id="c2c98-129">hello **백업을** 블레이드를 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c2c98-129">hello **Backups** blade will be displayed.</span></span>
   
    ![백업 페이지][ChooseBackupsPage]
   
   > [!NOTE]
   > <span data-ttu-id="c2c98-131">아래 hello 메시지를 표시 하는 경우 클릭 하기 전에 앱 서비스 계획을 진행할 수 tooupgrade 백업으로.</span><span class="sxs-lookup"><span data-stu-id="c2c98-131">If you see hello message below, click it tooupgrade your App Service plan before you can proceed with backups.</span></span>
   > <span data-ttu-id="c2c98-132">자세한 내용은 [Azure에서 앱 확장](web-sites-scale.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c2c98-132">See [Scale up an app in Azure](web-sites-scale.md) for more information.</span></span>  
   > <span data-ttu-id="c2c98-133">![저장소 계정 선택](./media/web-sites-backup/01UpgradePlan1.png)</span><span class="sxs-lookup"><span data-stu-id="c2c98-133">![Choose storage account](./media/web-sites-backup/01UpgradePlan1.png)</span></span>
   > 
   > 

2. <span data-ttu-id="c2c98-134">Hello에 **백업** 블레이드에서 클릭 **구성**
![구성 클릭](./media/web-sites-backup/ClickConfigure1.png)</span><span class="sxs-lookup"><span data-stu-id="c2c98-134">In hello **Backup** blade, Click **Configure**
![Click Configure](./media/web-sites-backup/ClickConfigure1.png)</span></span>
3. <span data-ttu-id="c2c98-135">Hello에 **백업 구성** 블레이드에서 클릭 **저장소: 구성 되지** tooconfigure 저장소 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="c2c98-135">In hello **Backup Configuration** blade, click **Storage: Not configured** tooconfigure a storage account.</span></span>
   
    ![저장소 계정 선택][ChooseStorageAccount]
4. <span data-ttu-id="c2c98-137">**저장소 계정** 및 **컨테이너**를 선택하여 백업 대상을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c2c98-137">Choose your backup destination by selecting a **Storage Account** and **Container**.</span></span> <span data-ttu-id="c2c98-138">hello 저장소 계정이 toohello 속해야 tooback를 원하는 hello 앱과 동일한 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2c98-138">hello storage account must belong toohello same subscription as hello app you want tooback up.</span></span> <span data-ttu-id="c2c98-139">원하는 경우 해당 블레이드 hello에에서 새 저장소 계정 또는 새 컨테이너를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2c98-139">If you wish, you can create a new storage account or a new container in hello respective blades.</span></span> <span data-ttu-id="c2c98-140">완료되면 **선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c2c98-140">When you're done, click **Select**.</span></span>
   
    ![저장소 계정 선택](./media/web-sites-backup/02ChooseStorageAccount1-1.png)
5. <span data-ttu-id="c2c98-142">Hello에 **백업 구성** 구성할 수는 계속 열려 블레이드에서 **Backup Database**, tooinclude hello 백업 (SQL 데이터베이스 또는 MySQL)에 사용한 다음 클릭 hello 데이터베이스를 선택 합니다 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="c2c98-142">In hello **Backup Configuration** blade that is still left open, you can configure **Backup Database**, then select hello databases you want tooinclude in hello backups (SQL database or MySQL), then click **OK**.</span></span>  
   
    ![저장소 계정 선택](./media/web-sites-backup/03ConfigureDatabase1.png)
   
   > [!NOTE]
   > <span data-ttu-id="c2c98-144">이 목록에서 데이터베이스 tooappear에 대 한 연결 문자열 hello에 존재 해야 **연결 문자열** hello 섹션 **응용 프로그램 설정** 블레이드 앱에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2c98-144">For a database tooappear in this list, its connection string must exist in hello **Connection strings** section of hello **Application settings** blade for your app.</span></span>
   > 
   > 
6. <span data-ttu-id="c2c98-145">Hello에 **백업 구성** 블레이드에서 클릭 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="c2c98-145">In hello **Backup Configuration** blade, click **Save**.</span></span>    
7. <span data-ttu-id="c2c98-146">Hello에 **백업을** 블레이드에서 클릭 **백업**합니다.</span><span class="sxs-lookup"><span data-stu-id="c2c98-146">In hello  **Backups** blade, click **Backup**.</span></span>
   
    ![BackUpNow 단추][BackUpNow]
   
    <span data-ttu-id="c2c98-148">Hello 백업 프로세스 중 진행 메시지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2c98-148">You see a progress message during hello backup process.</span></span>

<span data-ttu-id="c2c98-149">Hello 저장소 계정 및 컨테이너 구성 되 면 언제 든 지 수동 백업을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2c98-149">Once hello storage account and container is configured you can initiate a manual backup at any time.</span></span>  

<a name="automatedbackups"></a>

## <a name="configure-automated-backups"></a><span data-ttu-id="c2c98-150">자동화된 백업 구성</span><span class="sxs-lookup"><span data-stu-id="c2c98-150">Configure automated backups</span></span>
1. <span data-ttu-id="c2c98-151">Hello에 **백업 구성** 설정 블레이드에서 **예약 된 백업** 너무**에**합니다.</span><span class="sxs-lookup"><span data-stu-id="c2c98-151">In hello **Backup Configuration** blade, set **Scheduled backup** too**On**.</span></span> 
   
    ![저장소 계정 선택](./media/web-sites-backup/05ScheduleBackup1.png)
2. <span data-ttu-id="c2c98-153">옵션 표시 됩니다, 백업 일정이 설정 **예약 된 백업** 너무**에**원하는 대로 hello 백업 일정을 구성 합니다. 다음을 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="c2c98-153">Backup schedule options will show up, set **Scheduled Backup** too**On**, then configure hello backup schedule as desired and click **OK**.</span></span>
   
    ![자동 백업 사용][SetAutomatedBackupOn]

<a name="partialbackups"></a>

## <a name="configure-partial-backups"></a><span data-ttu-id="c2c98-155">부분 백업 구성</span><span class="sxs-lookup"><span data-stu-id="c2c98-155">Configure Partial Backups</span></span>
<span data-ttu-id="c2c98-156">경우에 따라 원하지 toobackup 모든 앱에 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2c98-156">Sometimes you don't want toobackup everything on your app.</span></span> <span data-ttu-id="c2c98-157">다음은 몇 가지 예입니다.</span><span class="sxs-lookup"><span data-stu-id="c2c98-157">Here are a few examples:</span></span>

* <span data-ttu-id="c2c98-158">오래된 블로그 게시물이나 이미지처럼 변하지 않는 정적 콘텐츠가 포함된 앱의 [주별 백업을 설정](web-sites-backup.md#configure-automated-backups) 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2c98-158">You [set up weekly backups](web-sites-backup.md#configure-automated-backups) of your app that contains static content that never changes, such as old blog posts or images.</span></span>
* <span data-ttu-id="c2c98-159">응용 프로그램에 (즉, 한 번에 백업할 수 hello 최대 크기) 콘텐츠의 10GB 이상.</span><span class="sxs-lookup"><span data-stu-id="c2c98-159">Your app has over 10 GB of content (that's hello max amount you can backup at a time).</span></span>
* <span data-ttu-id="c2c98-160">Toobackup hello 로그 파일을 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c2c98-160">You don't want toobackup hello log files.</span></span>

<span data-ttu-id="c2c98-161">부분 백업 정확 하 게 하는 파일 수를 선택할 수 있습니다. 원하는 toobackup 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2c98-161">Partial backups allows you choose exactly which files you want toobackup.</span></span>

### <a name="exclude-files-from-your-backup"></a><span data-ttu-id="c2c98-162">백업에서 파일 제외</span><span class="sxs-lookup"><span data-stu-id="c2c98-162">Exclude files from your backup</span></span>
<span data-ttu-id="c2c98-163">로그 파일 및 정적 이미지를 한 번 백업 되 고 toochange 진행 되지 않고 있는 앱 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2c98-163">Suppose you have an app that contains log files and static images that have been backup once and are not going toochange.</span></span> <span data-ttu-id="c2c98-164">이러한 경우 해당 폴더와 파일을 이후의 백업에서 저장하지 않도록 제외할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2c98-164">In such cases you can exclude those folders and files from being stored in your future backups.</span></span> <span data-ttu-id="c2c98-165">tooexclude 파일과 하면 백업에서 폴더 만들기는 `_backup.filter` hello에 대 한 파일 `D:\home\site\wwwroot` 응용 프로그램의 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="c2c98-165">tooexclude files and folders from your backups, create a `_backup.filter` file in hello `D:\home\site\wwwroot` folder of your app.</span></span> <span data-ttu-id="c2c98-166">파일 및 폴더 tooexclude이이 파일에 원하는 hello 목록을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2c98-166">Specify hello list of files and folders you want tooexclude in this file.</span></span> 

<span data-ttu-id="c2c98-167">파일은 toouse Kudu는 쉽게 tooaccess 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2c98-167">An easy way tooaccess your files is toouse Kudu .</span></span> <span data-ttu-id="c2c98-168">클릭 **고급 도구 Go->** 웹 앱 tooaccess Kudu에 대 한 설정입니다.</span><span class="sxs-lookup"><span data-stu-id="c2c98-168">Click **Advanced Tools -> Go** setting for your web app tooaccess Kudu.</span></span>

![포털을 사용하는 Kudu][kudu-portal]

<span data-ttu-id="c2c98-170">백업에서 tooexclude 되도록 hello 폴더를 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2c98-170">Identify hello folders that you want tooexclude from your backups.</span></span>  <span data-ttu-id="c2c98-171">예를 들어 원하는 toofilter hello 강조 표시 된 폴더와 파일을 초과 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2c98-171">For example , you want toofilter out hello highlighted folder and files.</span></span>

![Images 폴더][ImagesFolder]

<span data-ttu-id="c2c98-173">파일을 만들 `_backup.filter` 위의 hello 목록 hello 파일에 저장 되지만 제거 및 `D:\home`합니다.</span><span class="sxs-lookup"><span data-stu-id="c2c98-173">Create a file called `_backup.filter` and put hello list above in hello file, but remove `D:\home`.</span></span> <span data-ttu-id="c2c98-174">줄당 하나의 디렉터리 또는 파일을 나열하세요.</span><span class="sxs-lookup"><span data-stu-id="c2c98-174">List one directory or file per line.</span></span> <span data-ttu-id="c2c98-175">따라서 hello 파일의 내용을 hello 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2c98-175">So hello content of hello file should be:</span></span>
 ```bash
    \site\wwwroot\Images\brand.png
    \site\wwwroot\Images\2014
    \site\wwwroot\Images\2013
```

<span data-ttu-id="c2c98-176">업로드 `_backup.filter` toohello 파일 `D:\home\site\wwwroot\` 사용 하 여 사이트의 디렉터리 [ftp](web-sites-deploy.md#ftp) 또는 다른 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="c2c98-176">Upload `_backup.filter` file toohello `D:\home\site\wwwroot\` directory of your site using [ftp](web-sites-deploy.md#ftp) or any other method.</span></span> <span data-ttu-id="c2c98-177">Kudu를 사용 하 여 직접 hello 파일을 만들 수 있습니다 `DebugConsole` 있습니다 hello 콘텐츠를 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2c98-177">If you wish, you can create hello file directly using Kudu  `DebugConsole` and insert hello content there.</span></span>

<span data-ttu-id="c2c98-178">동일한 실행된 백업을 hello 수행한 방식으로 일반적으로, [수동으로](#create-a-manual-backup) 또는 [자동으로](#configure-automated-backups)합니다.</span><span class="sxs-lookup"><span data-stu-id="c2c98-178">Run backups hello same way you would normally do it, [manually](#create-a-manual-backup) or [automatically](#configure-automated-backups).</span></span> <span data-ttu-id="c2c98-179">이제, 파일 및 폴더에 지정 된 `_backup.filter` hello 예약 하거나 수동으로 시작 된 이후 백업에서 제외 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c2c98-179">Now, any files and folders that are specified in `_backup.filter` is excluded from hello future backups scheduled or manually initiated.</span></span> 

> [!NOTE]
> <span data-ttu-id="c2c98-180">사이트 hello의 부분 백업을 복원 합니다. 같은 방법으로 [일반 백업 복원](web-sites-restore.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c2c98-180">You restore partial backups of your site hello same way you would [restore a regular backup](web-sites-restore.md).</span></span> <span data-ttu-id="c2c98-181">hello 복원 프로세스 가깝습니다를 안녕지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c2c98-181">hello restore process does hello right thing.</span></span>
> 
> <span data-ttu-id="c2c98-182">전체 백업이 복원 되 면 hello 사이트에서 모든 콘텐츠 hello 백업에 무엇이으로 바뀝니다.</span><span class="sxs-lookup"><span data-stu-id="c2c98-182">When a full backup is restored, all content on hello site is replaced with whatever is in hello backup.</span></span> <span data-ttu-id="c2c98-183">파일이 hello 사이트에 있지만 hello 백업에는 없는 경우 삭제를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="c2c98-183">If a file is on hello site, but not in hello backup it gets deleted.</span></span> <span data-ttu-id="c2c98-184">하지만 부분 백업 복원 되 면 hello 차단 목록에 포함할 디렉터리 중 하나 또는 모든 블랙 리스트에 올린된 파일에 있는 모든 콘텐츠에 있는 그대로 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c2c98-184">But when a partial backup is restored, any content that is located in one of hello blacklisted directories, or any blacklisted file, is left as is.</span></span>
> 


<a name="aboutbackups"></a>

## <a name="how-backups-are-stored"></a><span data-ttu-id="c2c98-185">백업 저장 방법</span><span class="sxs-lookup"><span data-stu-id="c2c98-185">How backups are stored</span></span>
<span data-ttu-id="c2c98-186">Hello 백업을 hello에 표시 되는 앱에 대 한 하나 이상의 백업을 수행한 후 **컨테이너** 저장소 계정과 응용 프로그램의 블레이드에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2c98-186">After you have made one or more backups for your app, hello backups are visible on hello **Containers** blade of your storage account, and your app.</span></span> <span data-ttu-id="c2c98-187">각 백업 이루어져 hello 저장소 계정에는`.zip` hello 백업 데이터를 포함 하는 파일 및 `.xml` hello의 매니페스트가 포함 된 파일 `.zip` 파일 내용의 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2c98-187">In hello storage account, each backup consists of a`.zip` file that contains hello backup data and an `.xml` file that contains a manifest of hello `.zip` file contents.</span></span> <span data-ttu-id="c2c98-188">압축을 풀 수 있으며 원하는 tooaccess 백업을 복원 하는 경우 응용 프로그램을 실제로 수행 하지 않고 경우 이러한 파일을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2c98-188">You can unzip and browse these files if you want tooaccess your backups without actually performing an app restore.</span></span>

<span data-ttu-id="c2c98-189">hello 앱에 대 한 데이터베이스 백업은 hello the.zip 파일의 hello 루트에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c2c98-189">hello database backup for hello app is stored in hello root of the.zip file.</span></span> <span data-ttu-id="c2c98-190">SQL 데이터베이스의 경우 이 파일은 BACPAC 파일(파일 확장명 없음)이며, 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2c98-190">For a SQL database, this is a BACPAC file (no file extension) and can be imported.</span></span> <span data-ttu-id="c2c98-191">toocreate hello BACPAC 내보내기에 따라 SQL 데이터베이스, 참조 [가져올 BACPAC 파일 tooCreate 새 사용자 데이터베이스](http://technet.microsoft.com/library/hh710052.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="c2c98-191">toocreate a SQL database based on hello BACPAC export, see [Import a BACPAC File tooCreate a New User Database](http://technet.microsoft.com/library/hh710052.aspx).</span></span>

> [!WARNING]
> <span data-ttu-id="c2c98-192">hello 파일을 변경 하면 **websitebackups** 컨테이너에 잘못 된 서명과 따라서 restorable 아닌 백업 toobecome hello 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2c98-192">Altering any of hello files in your **websitebackups** container can cause hello backup toobecome invalid and therefore non-restorable.</span></span>
> 
> 

<a name="nextsteps"></a>

## <a name="next-steps"></a><span data-ttu-id="c2c98-193">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c2c98-193">Next Steps</span></span>
<span data-ttu-id="c2c98-194">앱을 백업에서 복원하는 방법에 대한 자세한 내용은 [Azure에서 앱 복원](web-sites-restore.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c2c98-194">For information on restoring an app from a backup, see [Restore an app in Azure](web-sites-restore.md).</span></span> <span data-ttu-id="c2c98-195">백업 하 고 REST API를 사용 하 여 앱 서비스 앱을 복원할 수도 있습니다 (참조 [사용 REST toobackup 및 복원 앱 서비스 앱](websites-csm-backup.md)).</span><span class="sxs-lookup"><span data-stu-id="c2c98-195">You can also backup and restore App Service apps using REST API (see [Use REST toobackup and restore App Service apps](websites-csm-backup.md)).</span></span>


<!-- IMAGES -->
[ChooseBackupsPage]: ./media/web-sites-backup/01ChooseBackupsPage1.png
[ChooseStorageAccount]: ./media/web-sites-backup/02ChooseStorageAccount-1.png
[IncludedDatabases]: ./media/web-sites-backup/03IncludedDatabases.png
[BackUpNow]: ./media/web-sites-backup/04BackUpNow1.png
[BackupProgress]: ./media/web-sites-backup/05BackupProgress.png
[SetAutomatedBackupOn]: ./media/web-sites-backup/06SetAutomatedBackupOn1.png
[Frequency]: ./media/web-sites-backup/07Frequency.png
[StartDate]: ./media/web-sites-backup/08StartDate.png
[StartTime]: ./media/web-sites-backup/09StartTime.png
[SaveIcon]: ./media/web-sites-backup/10SaveIcon.png
[ImagesFolder]: ./media/web-sites-backup/11Images.png
[LogsFolder]: ./media/web-sites-backup/12Logs.png
[GhostUpgradeWarning]: ./media/web-sites-backup/13GhostUpgradeWarning.png
[kudu-portal]:./media/web-sites-backup/kudu-portal.PNG

