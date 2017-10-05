---
title: "Azure에서 앱 백업"
description: "Azure 앱 서비스에서 앱의 백업을 만드는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 77e983afaaba8e944ab1f337e1c28ced83b63205
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="back-up-your-app-in-azure"></a><span data-ttu-id="1b17e-103">Azure에서 앱 백업</span><span class="sxs-lookup"><span data-stu-id="1b17e-103">Back up your app in Azure</span></span>
<span data-ttu-id="1b17e-104">[Azure App Service](../app-service/app-service-value-prop-what-is.md)의 백업 및 복원 기능을 사용하여 수동으로 또는 일정에 따라 앱 백업을 쉽게 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b17e-104">The Back up and Restore feature in [Azure App Service](../app-service/app-service-value-prop-what-is.md) lets you easily create app backups manually or on a schedule.</span></span> <span data-ttu-id="1b17e-105">기존 앱을 덮어쓰거나 다른 앱으로 복원하여 앱을 이전 상태의 스냅숏으로 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b17e-105">You can restore the app to a snapshot of a previous state by overwriting the existing app or restoring to another app.</span></span> 

<span data-ttu-id="1b17e-106">앱을 백업에서 복원하는 방법에 대한 자세한 내용은 [Azure에서 앱 복원](web-sites-restore.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1b17e-106">For information on restoring an app from backup, see [Restore an app in Azure](web-sites-restore.md).</span></span>

<a name="whatsbackedup"></a>

## <a name="what-gets-backed-up"></a><span data-ttu-id="1b17e-107">백업 대상</span><span class="sxs-lookup"><span data-stu-id="1b17e-107">What gets backed up</span></span>
<span data-ttu-id="1b17e-108">App Service는 앱에서 사용하도록 구성한 Azure Storage 계정과 컨테이너에 다음 정보를 백업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b17e-108">App Service can backup the following information to an Azure storage account and container that you have configured your app to use.</span></span> 

* <span data-ttu-id="1b17e-109">앱 구성</span><span class="sxs-lookup"><span data-stu-id="1b17e-109">App configuration</span></span>
* <span data-ttu-id="1b17e-110">파일 콘텐츠</span><span class="sxs-lookup"><span data-stu-id="1b17e-110">File content</span></span>
* <span data-ttu-id="1b17e-111">앱에 연결된 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="1b17e-111">Database connected to your app</span></span>

<span data-ttu-id="1b17e-112">백업 기능과 함께 지원되는 데이터베이스 솔루션은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1b17e-112">The following database solutions are supported with backup feature:</span></span> 
   - [<span data-ttu-id="1b17e-113">SQL 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="1b17e-113">SQL Database</span></span>](https://azure.microsoft.com/en-us/services/sql-database/)
   - [<span data-ttu-id="1b17e-114">Azure Database for MySQL(미리 보기)</span><span class="sxs-lookup"><span data-stu-id="1b17e-114">Azure Database for MySQL (Preview)</span></span>](https://azure.microsoft.com/en-us/services/mysql)
   - [<span data-ttu-id="1b17e-115">Azure Database for PostgreSQL(미리 보기)</span><span class="sxs-lookup"><span data-stu-id="1b17e-115">Azure Database for PostgreSQL (Preview)</span></span>](https://azure.microsoft.com/en-us/services/postgres)
   - [<span data-ttu-id="1b17e-116">ClearDB MySQL</span><span class="sxs-lookup"><span data-stu-id="1b17e-116">ClearDB MySQL</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/SuccessBricksInc.ClearDBMySQLDatabase?tab=Overview)
   - [<span data-ttu-id="1b17e-117">MySQL 인앱</span><span class="sxs-lookup"><span data-stu-id="1b17e-117">MySQL in-app</span></span>](https://blogs.msdn.microsoft.com/appserviceteam/2017/03/06/announcing-general-availability-for-mysql-in-app)
 

> [!NOTE]
>  <span data-ttu-id="1b17e-118">각 백업은 증분 업데이트가 아니라 앱의 완전한 오프라인 복사본입니다.</span><span class="sxs-lookup"><span data-stu-id="1b17e-118">Each backup is a complete offline copy of your app, not an incremental update.</span></span>
>  

<a name="requirements"></a>

## <a name="requirements-and-restrictions"></a><span data-ttu-id="1b17e-119">요구 사항 및 제한 사항</span><span class="sxs-lookup"><span data-stu-id="1b17e-119">Requirements and restrictions</span></span>
* <span data-ttu-id="1b17e-120">백업 및 복원 기능을 사용하려면 App Service 계획이 **표준** 계층 또는 **프리미엄** 계층에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b17e-120">The Back up and Restore feature requires the App Service plan to be in the **Standard** tier or **Premium** tier.</span></span> <span data-ttu-id="1b17e-121">더 높은 계층을 사용하도록 앱 서비스 계획을 확장하는 방법에 대한 자세한 내용은 [Azure에서 앱 확장](web-sites-scale.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1b17e-121">For more information about scaling your App Service plan to use a higher tier, see [Scale up an app in Azure](web-sites-scale.md).</span></span>  
  <span data-ttu-id="1b17e-122">**프리미엄** 계층을 사용하면 **표준** 계층보다 더 많은 매일 백업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b17e-122">**Premium** tier allows a greater number of daily back ups than **Standard** tier.</span></span>
* <span data-ttu-id="1b17e-123">Azure 저장소 계정과 컨테이너가 백업하려는 앱과 동일한 구독에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b17e-123">You need an Azure storage account and container in the same subscription as the app that you want to backup.</span></span> <span data-ttu-id="1b17e-124">Azure 저장소 계정에 대한 자세한 내용은 이 문서의 끝에 있는 [링크](#moreaboutstorage) 를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="1b17e-124">For more information on Azure storage accounts, see the [links](#moreaboutstorage) at the end of this article.</span></span>
* <span data-ttu-id="1b17e-125">최대 10GB의 앱 및 데이터베이스 콘텐츠를 백업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b17e-125">Backups can be up to 10 GB of app and database content.</span></span> <span data-ttu-id="1b17e-126">백업 크기가 이 제한을 초과하면 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="1b17e-126">If the backup size exceeds this limit, you get an error .</span></span>

<a name="manualbackup"></a>

## <a name="create-a-manual-backup"></a><span data-ttu-id="1b17e-127">수동 백업 만들기</span><span class="sxs-lookup"><span data-stu-id="1b17e-127">Create a manual backup</span></span>
1. <span data-ttu-id="1b17e-128">[Azure Portal](https://portal.azure.com)에서 앱의 블레이드로 이동하여 **백업**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1b17e-128">In the [Azure Portal](https://portal.azure.com), navigate to your app's blade, select **Backups**.</span></span> <span data-ttu-id="1b17e-129">**백업** 블레이드가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b17e-129">The **Backups** blade will be displayed.</span></span>
   
    ![백업 페이지][ChooseBackupsPage]
   
   > [!NOTE]
   > <span data-ttu-id="1b17e-131">아래와 같은 메시지가 나타나면 백업을 계속 진행하기 전에 클릭하여 앱 서비스 계획을 업그레이드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b17e-131">If you see the message below, click it to upgrade your App Service plan before you can proceed with backups.</span></span>
   > <span data-ttu-id="1b17e-132">자세한 내용은 [Azure에서 앱 확장](web-sites-scale.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1b17e-132">See [Scale up an app in Azure](web-sites-scale.md) for more information.</span></span>  
   > <span data-ttu-id="1b17e-133">![저장소 계정 선택](./media/web-sites-backup/01UpgradePlan1.png)</span><span class="sxs-lookup"><span data-stu-id="1b17e-133">![Choose storage account](./media/web-sites-backup/01UpgradePlan1.png)</span></span>
   > 
   > 

2. <span data-ttu-id="1b17e-134">**백업** 블레이드에서 **구성** 클릭
![구성 클릭](./media/web-sites-backup/ClickConfigure1.png)</span><span class="sxs-lookup"><span data-stu-id="1b17e-134">In the **Backup** blade, Click **Configure**
![Click Configure](./media/web-sites-backup/ClickConfigure1.png)</span></span>
3. <span data-ttu-id="1b17e-135">**백업 구성** 블레이드에서 **저장소: 구성되지 않음**을 클릭하여 저장소 계정을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="1b17e-135">In the **Backup Configuration** blade, click **Storage: Not configured** to configure a storage account.</span></span>
   
    ![저장소 계정 선택][ChooseStorageAccount]
4. <span data-ttu-id="1b17e-137">**저장소 계정** 및 **컨테이너**를 선택하여 백업 대상을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1b17e-137">Choose your backup destination by selecting a **Storage Account** and **Container**.</span></span> <span data-ttu-id="1b17e-138">저장소 계정은 백업할 앱이 있는 동일한 구독에 속해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b17e-138">The storage account must belong to the same subscription as the app you want to back up.</span></span> <span data-ttu-id="1b17e-139">필요한 경우 각 블레이드에서 새 저장소 계정이 나 새 컨테이너를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b17e-139">If you wish, you can create a new storage account or a new container in the respective blades.</span></span> <span data-ttu-id="1b17e-140">완료되면 **선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1b17e-140">When you're done, click **Select**.</span></span>
   
    ![저장소 계정 선택](./media/web-sites-backup/02ChooseStorageAccount1-1.png)
5. <span data-ttu-id="1b17e-142">왼쪽에 열려 있는 **백업 구성** 블레이드에서 **데이터베이스 백업**을 구성한 다음 백업에 포함할 데이터베이스(SQL Database 또는 MySQL)를 선택하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1b17e-142">In the **Backup Configuration** blade that is still left open, you can configure **Backup Database**, then select the databases you want to include in the backups (SQL database or MySQL), then click **OK**.</span></span>  
   
    ![저장소 계정 선택](./media/web-sites-backup/03ConfigureDatabase1.png)
   
   > [!NOTE]
   > <span data-ttu-id="1b17e-144">이 목록에 표시될 데이터베이스의 경우 연결 문자열은 앱의 **응용 프로그램 설정** 블레이드에서 **연결 문자열** 섹션에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b17e-144">For a database to appear in this list, its connection string must exist in the **Connection strings** section of the **Application settings** blade for your app.</span></span>
   > 
   > 
6. <span data-ttu-id="1b17e-145">**백업 구성** 블레이드에서 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1b17e-145">In the **Backup Configuration** blade, click **Save**.</span></span>    
7. <span data-ttu-id="1b17e-146">**백업** 블레이드에서 **백업**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1b17e-146">In the  **Backups** blade, click **Backup**.</span></span>
   
    ![BackUpNow 단추][BackUpNow]
   
    <span data-ttu-id="1b17e-148">백업 프로세스를 수행하는 동안 진행 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b17e-148">You see a progress message during the backup process.</span></span>

<span data-ttu-id="1b17e-149">저장소 계정과 컨테이너가 구성되면 언제든지 수동 백업을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b17e-149">Once the storage account and container is configured you can initiate a manual backup at any time.</span></span>  

<a name="automatedbackups"></a>

## <a name="configure-automated-backups"></a><span data-ttu-id="1b17e-150">자동화된 백업 구성</span><span class="sxs-lookup"><span data-stu-id="1b17e-150">Configure automated backups</span></span>
1. <span data-ttu-id="1b17e-151">**백업 구성** 블레이드에서 **예약된 백업**을 **켜기**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="1b17e-151">In the **Backup Configuration** blade, set **Scheduled backup** to **On**.</span></span> 
   
    ![저장소 계정 선택](./media/web-sites-backup/05ScheduleBackup1.png)
2. <span data-ttu-id="1b17e-153">백업 일정 옵션이 표시되면 **예약된 백업**을 **켜기**로 설정하고 원하는 대로 백업 일정을 구성한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1b17e-153">Backup schedule options will show up, set **Scheduled Backup** to **On**, then configure the backup schedule as desired and click **OK**.</span></span>
   
    ![자동 백업 사용][SetAutomatedBackupOn]

<a name="partialbackups"></a>

## <a name="configure-partial-backups"></a><span data-ttu-id="1b17e-155">부분 백업 구성</span><span class="sxs-lookup"><span data-stu-id="1b17e-155">Configure Partial Backups</span></span>
<span data-ttu-id="1b17e-156">앱의 모든 것을 백업하고 싶지 않을 때도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b17e-156">Sometimes you don't want to backup everything on your app.</span></span> <span data-ttu-id="1b17e-157">다음은 몇 가지 예입니다.</span><span class="sxs-lookup"><span data-stu-id="1b17e-157">Here are a few examples:</span></span>

* <span data-ttu-id="1b17e-158">오래된 블로그 게시물이나 이미지처럼 변하지 않는 정적 콘텐츠가 포함된 앱의 [주별 백업을 설정](web-sites-backup.md#configure-automated-backups) 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b17e-158">You [set up weekly backups](web-sites-backup.md#configure-automated-backups) of your app that contains static content that never changes, such as old blog posts or images.</span></span>
* <span data-ttu-id="1b17e-159">앱의 콘텐츠가 10GB 이상이며, 이는 한 번에 백업할 수 있는 최대 용량입니다.</span><span class="sxs-lookup"><span data-stu-id="1b17e-159">Your app has over 10 GB of content (that's the max amount you can backup at a time).</span></span>
* <span data-ttu-id="1b17e-160">로그 파일은 백업할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1b17e-160">You don't want to backup the log files.</span></span>

<span data-ttu-id="1b17e-161">부분 백업을 사용하면 백업할 파일을 정확히 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b17e-161">Partial backups allows you choose exactly which files you want to backup.</span></span>

### <a name="exclude-files-from-your-backup"></a><span data-ttu-id="1b17e-162">백업에서 파일 제외</span><span class="sxs-lookup"><span data-stu-id="1b17e-162">Exclude files from your backup</span></span>
<span data-ttu-id="1b17e-163">한 번 백업되었고 변경하지 않을 로그 파일과 정적 이미지가 포함된 앱이 있다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="1b17e-163">Suppose you have an app that contains log files and static images that have been backup once and are not going to change.</span></span> <span data-ttu-id="1b17e-164">이러한 경우 해당 폴더와 파일을 이후의 백업에서 저장하지 않도록 제외할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b17e-164">In such cases you can exclude those folders and files from being stored in your future backups.</span></span> <span data-ttu-id="1b17e-165">백업에서 파일과 폴더를 제외하려면 앱의 `D:\home\site\wwwroot` 폴더에 `_backup.filter` 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1b17e-165">To exclude files and folders from your backups, create a `_backup.filter` file in the `D:\home\site\wwwroot` folder of your app.</span></span> <span data-ttu-id="1b17e-166">이 파일에서 제외할 파일과 폴더의 목록을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="1b17e-166">Specify the list of files and folders you want to exclude in this file.</span></span> 

<span data-ttu-id="1b17e-167">파일에 쉽게 액세스하는 방법은 Kudu를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1b17e-167">An easy way to access your files is to use Kudu .</span></span> <span data-ttu-id="1b17e-168">Kudu에 액세스하려면 웹앱의 **고급 도구 -> 이동** 설정을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1b17e-168">Click **Advanced Tools -> Go** setting for your web app to access Kudu.</span></span>

![포털을 사용하는 Kudu][kudu-portal]

<span data-ttu-id="1b17e-170">백업에서 제외하려는 폴더를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="1b17e-170">Identify the folders that you want to exclude from your backups.</span></span>  <span data-ttu-id="1b17e-171">예를 들어 강조 표시된 폴더와 파일을 필터링하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b17e-171">For example , you want to filter out the highlighted folder and files.</span></span>

![Images 폴더][ImagesFolder]

<span data-ttu-id="1b17e-173">`_backup.filter`라는 파일을 만들고 위 목록을 파일에 저장하지만 `D:\home`을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="1b17e-173">Create a file called `_backup.filter` and put the list above in the file, but remove `D:\home`.</span></span> <span data-ttu-id="1b17e-174">줄당 하나의 디렉터리 또는 파일을 나열하세요.</span><span class="sxs-lookup"><span data-stu-id="1b17e-174">List one directory or file per line.</span></span> <span data-ttu-id="1b17e-175">파일의 내용은 다음과 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b17e-175">So the content of the file should be:</span></span>
 ```bash
    \site\wwwroot\Images\brand.png
    \site\wwwroot\Images\2014
    \site\wwwroot\Images\2013
```

<span data-ttu-id="1b17e-176">[ftp](web-sites-deploy.md#ftp) 또는 다른 방법을 사용하여 해당 사이트의 `D:\home\site\wwwroot\` 디렉터리에 `_backup.filter` 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="1b17e-176">Upload `_backup.filter` file to the `D:\home\site\wwwroot\` directory of your site using [ftp](web-sites-deploy.md#ftp) or any other method.</span></span> <span data-ttu-id="1b17e-177">필요한 경우 `DebugConsole` Kudu를 사용하여 파일을 직접 만들고 여기에 내용을 삽입할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b17e-177">If you wish, you can create the file directly using Kudu  `DebugConsole` and insert the content there.</span></span>

<span data-ttu-id="1b17e-178">이제 평소와 같이 [수동](#create-a-manual-backup) 또는 [자동](#configure-automated-backups)으로 백업을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1b17e-178">Run backups the same way you would normally do it, [manually](#create-a-manual-backup) or [automatically](#configure-automated-backups).</span></span> <span data-ttu-id="1b17e-179">이제 `_backup.filter`에 지정된 파일과 폴더가 이후에 예약되거나 수동으로 시작되는 백업에서 제외됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b17e-179">Now, any files and folders that are specified in `_backup.filter` is excluded from the future backups scheduled or manually initiated.</span></span> 

> [!NOTE]
> <span data-ttu-id="1b17e-180">[정기 백업을 복원](web-sites-restore.md)할 때와 동일한 방법으로 사이트의 부분 백업을 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="1b17e-180">You restore partial backups of your site the same way you would [restore a regular backup](web-sites-restore.md).</span></span> <span data-ttu-id="1b17e-181">복원 프로세스는 올바르게 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b17e-181">The restore process does the right thing.</span></span>
> 
> <span data-ttu-id="1b17e-182">전체 백업이 복원되면 해당 사이트의 모든 콘텐츠가 백업에 있는 항목들로 대체됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b17e-182">When a full backup is restored, all content on the site is replaced with whatever is in the backup.</span></span> <span data-ttu-id="1b17e-183">파일이 사이트에 있지만 백업에 없는 경우 해당 파일은 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b17e-183">If a file is on the site, but not in the backup it gets deleted.</span></span> <span data-ttu-id="1b17e-184">하지만 부분 백업이 복원되면 블랙 리스트 디렉터리에 위치한 모든 콘텐츠 또는 블랙 리스트에 포함된 모든 파일이 그대로 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b17e-184">But when a partial backup is restored, any content that is located in one of the blacklisted directories, or any blacklisted file, is left as is.</span></span>
> 


<a name="aboutbackups"></a>

## <a name="how-backups-are-stored"></a><span data-ttu-id="1b17e-185">백업 저장 방법</span><span class="sxs-lookup"><span data-stu-id="1b17e-185">How backups are stored</span></span>
<span data-ttu-id="1b17e-186">앱에 대해 하나 이상의 백업을 만들면 저장소 계정의 **컨테이너** 블레이드와 앱에 해당 백업이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b17e-186">After you have made one or more backups for your app, the backups are visible on the **Containers** blade of your storage account, and your app.</span></span> <span data-ttu-id="1b17e-187">저장소 계정에서 각 백업은 백업 데이터가 포함된 `.zip` 파일과 해당 `.zip` 파일 콘텐츠의 매니페스트가 포함된 `.xml` 파일로 구성되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b17e-187">In the storage account, each backup consists of a`.zip` file that contains the backup data and an `.xml` file that contains a manifest of the `.zip` file contents.</span></span> <span data-ttu-id="1b17e-188">실제로 앱 복원을 수행하지 않고 백업에 액세스하고자 한다면 이들 파일의 압축을 풀고 찾아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b17e-188">You can unzip and browse these files if you want to access your backups without actually performing an app restore.</span></span>

<span data-ttu-id="1b17e-189">앱에 대한 데이터베이스 백업은 .zip 파일의 루트에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b17e-189">The database backup for the app is stored in the root of the.zip file.</span></span> <span data-ttu-id="1b17e-190">SQL 데이터베이스의 경우 이 파일은 BACPAC 파일(파일 확장명 없음)이며, 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b17e-190">For a SQL database, this is a BACPAC file (no file extension) and can be imported.</span></span> <span data-ttu-id="1b17e-191">BACPAC 내보내기를 기반으로 하여 SQL 데이터베이스를 만들려면 [BACPAC 파일을 가져와 새 사용자 데이터베이스 만들기](http://technet.microsoft.com/library/hh710052.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1b17e-191">To create a SQL database based on the BACPAC export, see [Import a BACPAC File to Create a New User Database](http://technet.microsoft.com/library/hh710052.aspx).</span></span>

> [!WARNING]
> <span data-ttu-id="1b17e-192">**websitebackups** 컨테이너에 있는 파일을 변경하면 백업이 잘못되어 복원할 수 없게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b17e-192">Altering any of the files in your **websitebackups** container can cause the backup to become invalid and therefore non-restorable.</span></span>
> 
> 

<a name="nextsteps"></a>

## <a name="next-steps"></a><span data-ttu-id="1b17e-193">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1b17e-193">Next Steps</span></span>
<span data-ttu-id="1b17e-194">앱을 백업에서 복원하는 방법에 대한 자세한 내용은 [Azure에서 앱 복원](web-sites-restore.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1b17e-194">For information on restoring an app from a backup, see [Restore an app in Azure](web-sites-restore.md).</span></span> <span data-ttu-id="1b17e-195">또한 REST API를 사용하여 App Service 앱을 백업하고 복원할 수 있습니다([REST를 사용하여 App Service 앱 백업 및 복원](websites-csm-backup.md)참조).</span><span class="sxs-lookup"><span data-stu-id="1b17e-195">You can also backup and restore App Service apps using REST API (see [Use REST to backup and restore App Service apps](websites-csm-backup.md)).</span></span>


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

