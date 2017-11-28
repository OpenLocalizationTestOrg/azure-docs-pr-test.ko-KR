---
title: "aaaRestore Azure에서 응용 프로그램"
description: "자세한 내용은 방법 toorestore 백업에서 응용 프로그램입니다."
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: jimbe
ms.assetid: 4444dbf7-363c-47e2-b24a-dbd45cb08491
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2016
ms.author: cephalin
ms.openlocfilehash: 4b54029a9197064f990f29a3c4558c8322668714
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="restore-an-app-in-azure"></a><span data-ttu-id="f4764-103">Azure에서 앱 복원</span><span class="sxs-lookup"><span data-stu-id="f4764-103">Restore an app in Azure</span></span>
<span data-ttu-id="f4764-104">표시 하는이 문서에서 응용 프로그램 toorestore [Azure 앱 서비스](../app-service/app-service-value-prop-what-is.md) 을 이전에 백업 하는 (참조 [Azure에서 응용 프로그램을 백업](web-sites-backup.md)).</span><span class="sxs-lookup"><span data-stu-id="f4764-104">This article shows you how toorestore an app in [Azure App Service](../app-service/app-service-value-prop-what-is.md) that you have previously backed up (see [Back up your app in Azure](web-sites-backup.md)).</span></span> <span data-ttu-id="f4764-105">응용 프로그램을 연결 된 데이터베이스 요청 시 tooa 이전 상태로 복원 하거나 원래 응용 프로그램의 백업 중 하나에 따라 새 응용 프로그램을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4764-105">You can restore your app with its linked databases on-demand tooa previous state, or create a new app based on one of your original app's backup.</span></span> <span data-ttu-id="f4764-106">Azure 앱 서비스는 hello 다음 백업 및 복원에 대 한 데이터베이스를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4764-106">Azure App Service supports hello following databases for backup and restore:</span></span>
- [<span data-ttu-id="f4764-107">SQL 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="f4764-107">SQL Database</span></span>](https://azure.microsoft.com/en-us/services/sql-database/)
- [<span data-ttu-id="f4764-108">Azure Database for MySQL(미리 보기)</span><span class="sxs-lookup"><span data-stu-id="f4764-108">Azure Database for MySQL (Preview)</span></span>](https://azure.microsoft.com/en-us/services/mysql)
- [<span data-ttu-id="f4764-109">Azure Database for PostgreSQL(미리 보기)</span><span class="sxs-lookup"><span data-stu-id="f4764-109">Azure Database for PostgreSQL (Preview)</span></span>](https://azure.microsoft.com/en-us/services/postgres)
- [<span data-ttu-id="f4764-110">ClearDB MySQL</span><span class="sxs-lookup"><span data-stu-id="f4764-110">ClearDB MySQL</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/SuccessBricksInc.ClearDBMySQLDatabase?tab=Overview)
- [<span data-ttu-id="f4764-111">MySQL 인앱</span><span class="sxs-lookup"><span data-stu-id="f4764-111">MySQL in-app</span></span>](https://blogs.msdn.microsoft.com/appserviceteam/2017/03/06/announcing-general-availability-for-mysql-in-app)

<span data-ttu-id="f4764-112">백업에서 복원 작업은에서 실행 되는 사용 가능한 tooapps **표준** 및 **프리미엄** 계층입니다.</span><span class="sxs-lookup"><span data-stu-id="f4764-112">Restoring from backups is available tooapps running in **Standard** and **Premium** tier.</span></span> <span data-ttu-id="f4764-113">앱 확장에 대한 자세한 내용은 [Azure에서 앱 확장](web-sites-scale.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f4764-113">For information about scaling up your app, see [Scale up an app in Azure](web-sites-scale.md).</span></span> <span data-ttu-id="f4764-114">**프리미엄** 계층에서 더 많은 보다 수행 매일 백업 toobe의 허용 **표준** 계층입니다.</span><span class="sxs-lookup"><span data-stu-id="f4764-114">**Premium** tier allows a greater number of daily backups toobe performed than **Standard** tier.</span></span>

<a name="PreviousBackup"></a>

## <a name="restore-an-app-from-an-existing-backup"></a><span data-ttu-id="f4764-115">기존 백업에서 앱 복원</span><span class="sxs-lookup"><span data-stu-id="f4764-115">Restore an app from an existing backup</span></span>
1. <span data-ttu-id="f4764-116">Hello에 **설정** hello Azure 포털에서에서 응용 프로그램의 블레이드에서 클릭 **백업을** toodisplay hello **백업을** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="f4764-116">On hello **Settings** blade of your app in hello Azure Portal, click **Backups** toodisplay hello **Backups** blade.</span></span> <span data-ttu-id="f4764-117">그런 다음 **복원**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f4764-117">Then click **Restore**.</span></span>
   
    ![지금 복원 선택][ChooseRestoreNow]
2. <span data-ttu-id="f4764-119">Hello에 **복원** 블레이드, 첫 번째 select hello 백업 원본입니다.</span><span class="sxs-lookup"><span data-stu-id="f4764-119">In hello **Restore** blade, first select hello backup source.</span></span>
   
    ![](./media/web-sites-restore/021ChooseSource1.png)
   
    <span data-ttu-id="f4764-120">hello **응용 프로그램 백업** 옵션을 보면 모든 hello hello 현재 응용 프로그램의 기존 백업 및 쉽게 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4764-120">hello **App backup** option shows you all hello existing backups of hello current app, and you can easily select one.</span></span>
    <span data-ttu-id="f4764-121">hello **저장소** 옵션을 사용 하면 모든 기존 Azure 저장소 계정 및 구독에서 컨테이너에서 모든 백업 ZIP 파일을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4764-121">hello **Storage** option lets you select any backup ZIP file from any existing Azure Storage account and container in your subscription.</span></span>
    <span data-ttu-id="f4764-122">다른 응용 프로그램의 백업을 toorestore 중 어느 것을 사용 하 여 hello **저장소** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="f4764-122">If you're trying toorestore a backup of another app, use hello **Storage** option.</span></span>
3. <span data-ttu-id="f4764-123">그런 다음에 응용 프로그램 복원 hello에 대 한 hello 대상 지정 **복원 대상**합니다.</span><span class="sxs-lookup"><span data-stu-id="f4764-123">Then, specify hello destination for hello app restore in **Restore destination**.</span></span>
   
    ![](./media/web-sites-restore/022ChooseDestination1.png)
   
   > [!WARNING]
   > <span data-ttu-id="f4764-124">**덮어쓰기**를 선택하면 현재 앱의 기존 데이터를 모두 지우고 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="f4764-124">If you choose **Overwrite**, all existing data in your current app is erased and overwritten.</span></span> <span data-ttu-id="f4764-125">클릭 하기 전에 **확인**, 인지 정확 하 게 수행할 수 있는지 toodo 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4764-125">Before you click **OK**, make sure that it is exactly what you want toodo.</span></span>
   > 
   > 
   
    <span data-ttu-id="f4764-126">선택할 수 있습니다 **기존 앱** hello toorestore hello 응용 프로그램 백업 tooanother 앱 같은 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="f4764-126">You can select **Existing App** toorestore hello app backup tooanother app in hello same resoure group.</span></span> <span data-ttu-id="f4764-127">이 옵션을 사용 하기 전에 해야 이미 만든 다른 응용 프로그램 hello 응용 프로그램 백업에 정의 된 데이터베이스 구성 toohello 미러링을 사용 하 여 리소스 그룹에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4764-127">Before you use this option, you should have already created another app in your resource group with mirroring database configuration toohello one defined in hello app backup.</span></span> <span data-ttu-id="f4764-128">만들 수도 있습니다는 **새로** 앱 toorestore에 콘텐츠를 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4764-128">You can also Create a **New** app toorestore your content to.</span></span>

4. <span data-ttu-id="f4764-129">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f4764-129">Click **OK**.</span></span>

<a name="StorageAccount"></a>

## <a name="download-or-delete-a-backup-from-a-storage-account"></a><span data-ttu-id="f4764-130">저장소 계정에서 백업 다운로드 또는 삭제</span><span class="sxs-lookup"><span data-stu-id="f4764-130">Download or delete a backup from a storage account</span></span>
1. <span data-ttu-id="f4764-131">주 hello에서 **찾아보기** hello Azure 포털의 블레이드에서 **저장소 계정은**합니다.</span><span class="sxs-lookup"><span data-stu-id="f4764-131">From hello main **Browse** blade of hello Azure portal, select **Storage accounts**.</span></span> <span data-ttu-id="f4764-132">기존 저장소 계정 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4764-132">A list of your existing storage accounts is displayed.</span></span>
2. <span data-ttu-id="f4764-133">Toodownload 또는 delete.hello 블레이드 hello 저장소 계정에 대해 표시 되는 hello 백업을 포함 하는 hello 저장소 계정을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4764-133">Select hello storage account that contains hello backup that you want toodownload or delete.hello blade for hello storage account is displayed.</span></span>
3. <span data-ttu-id="f4764-134">저장소 계정 블레이드에서 hello hello 컨테이너 선택</span><span class="sxs-lookup"><span data-stu-id="f4764-134">In hello storage account blade, select hello container you want</span></span>
   
    ![컨테이너 보기][ViewContainers]
4. <span data-ttu-id="f4764-136">Toodownload 하거나 삭제할 백업 파일을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4764-136">Select backup file you want toodownload or delete.</span></span>
   
    ![ViewContainers](./media/web-sites-restore/03ViewFiles.png)
5. <span data-ttu-id="f4764-138">클릭 **다운로드** 또는 **삭제** 내역에 따라 원하는 toodo 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4764-138">Click **Download** or **Delete** depending on what you want toodo.</span></span>  

<a name="OperationLogs"></a>

## <a name="monitor-a-restore-operation"></a><span data-ttu-id="f4764-139">복원 작업 모니터링</span><span class="sxs-lookup"><span data-stu-id="f4764-139">Monitor a restore operation</span></span>
<span data-ttu-id="f4764-140">hello 응용 프로그램 복원 작업의 hello 성공 또는 실패에 대 한 세부 정보 toosee 이동 toohello **활동 로그** 블레이드 hello Azure 포털의에서.</span><span class="sxs-lookup"><span data-stu-id="f4764-140">toosee details about hello success or failure of hello app restore operation, navigate toohello **Activity Log** blade in hello Azure portal.</span></span>  
 

<span data-ttu-id="f4764-141">아래로 스크롤하여 toofind hello 원하는 복원 작업을 클릭 tooselect 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f4764-141">Scroll down toofind hello desired restore operation and click tooselect it.</span></span>

<span data-ttu-id="f4764-142">hello 세부 정보 블레이드에서 표시 hello 사용 가능한 관련 toohello 복원 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4764-142">hello details blade displays hello available information related toohello restore operation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f4764-143">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f4764-143">Next Steps</span></span>
<span data-ttu-id="f4764-144">백업 및 REST API를 사용 하 여 앱 서비스 앱을 복원할 수 있습니다 (참조 [사용 REST tooback 앱 서비스 앱을 복원 및](websites-csm-backup.md)).</span><span class="sxs-lookup"><span data-stu-id="f4764-144">You can backup and restore App Service apps using REST API (see [Use REST tooback up and restore App Service apps](websites-csm-backup.md)).</span></span>


<!-- IMAGES -->
[ChooseRestoreNow]: ./media/web-sites-restore/02ChooseRestoreNow1.png
[ViewContainers]: ./media/web-sites-restore/03ViewContainers.png
[StorageAccountFile]: ./media/web-sites-restore/02StorageAccountFile.png
[BrowseCloudStorage]: ./media/web-sites-restore/03BrowseCloudStorage.png
[StorageAccountFileSelected]: ./media/web-sites-restore/04StorageAccountFileSelected.png
[ChooseRestoreSettings]: ./media/web-sites-restore/05ChooseRestoreSettings.png
[ChooseDBServer]: ./media/web-sites-restore/06ChooseDBServer.png
[RestoreToNewSQLDB]: ./media/web-sites-restore/07RestoreToNewSQLDB.png
[NewSQLDBConfig]: ./media/web-sites-restore/08NewSQLDBConfig.png
[RestoredContosoWebSite]: ./media/web-sites-restore/09RestoredContosoWebSite.png
[DashboardOperationLogsLink]: ./media/web-sites-restore/10DashboardOperationLogsLink.png
[ManagementServicesOperationLogsList]: ./media/web-sites-restore/11ManagementServicesOperationLogsList.png
[DetailsButton]: ./media/web-sites-restore/12DetailsButton.png
[OperationDetails]: ./media/web-sites-restore/13OperationDetails.png
