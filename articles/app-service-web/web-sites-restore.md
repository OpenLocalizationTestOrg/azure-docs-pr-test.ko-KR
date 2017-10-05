---
title: "Azure에서 앱 복원"
description: "백업에서 앱을 복원하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 5fe74d992edb7028fa4a2500e427013d98ebc250
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="restore-an-app-in-azure"></a><span data-ttu-id="384a7-103">Azure에서 앱 복원</span><span class="sxs-lookup"><span data-stu-id="384a7-103">Restore an app in Azure</span></span>
<span data-ttu-id="384a7-104">이 문서에서는 이전에 백업한 [Azure App Service](../app-service/app-service-value-prop-what-is.md)에서 앱을 복원하는 방법을 보여 줍니다([Azure에서 앱 백업](web-sites-backup.md) 참조).</span><span class="sxs-lookup"><span data-stu-id="384a7-104">This article shows you how to restore an app in [Azure App Service](../app-service/app-service-value-prop-what-is.md) that you have previously backed up (see [Back up your app in Azure](web-sites-backup.md)).</span></span> <span data-ttu-id="384a7-105">요청 시 연결된 데이터베이스와 함께 앱을 이전 상태로 복원하거나, 원래 앱의 백업 중 하나를 기반으로 하여 새 앱을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="384a7-105">You can restore your app with its linked databases on-demand to a previous state, or create a new app based on one of your original app's backup.</span></span> <span data-ttu-id="384a7-106">Azure App Service는 백업 및 복원을 위해 다음과 같은 데이터베이스를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="384a7-106">Azure App Service supports the following databases for backup and restore:</span></span>
- [<span data-ttu-id="384a7-107">SQL 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="384a7-107">SQL Database</span></span>](https://azure.microsoft.com/en-us/services/sql-database/)
- [<span data-ttu-id="384a7-108">Azure Database for MySQL(미리 보기)</span><span class="sxs-lookup"><span data-stu-id="384a7-108">Azure Database for MySQL (Preview)</span></span>](https://azure.microsoft.com/en-us/services/mysql)
- [<span data-ttu-id="384a7-109">Azure Database for PostgreSQL(미리 보기)</span><span class="sxs-lookup"><span data-stu-id="384a7-109">Azure Database for PostgreSQL (Preview)</span></span>](https://azure.microsoft.com/en-us/services/postgres)
- [<span data-ttu-id="384a7-110">ClearDB MySQL</span><span class="sxs-lookup"><span data-stu-id="384a7-110">ClearDB MySQL</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/SuccessBricksInc.ClearDBMySQLDatabase?tab=Overview)
- [<span data-ttu-id="384a7-111">MySQL 인앱</span><span class="sxs-lookup"><span data-stu-id="384a7-111">MySQL in-app</span></span>](https://blogs.msdn.microsoft.com/appserviceteam/2017/03/06/announcing-general-availability-for-mysql-in-app)

<span data-ttu-id="384a7-112">백업에서 복원하는 방식은 **표준** 및 **프리미엄** 계층에서 실행되는 앱에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="384a7-112">Restoring from backups is available to apps running in **Standard** and **Premium** tier.</span></span> <span data-ttu-id="384a7-113">앱 확장에 대한 자세한 내용은 [Azure에서 앱 확장](web-sites-scale.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="384a7-113">For information about scaling up your app, see [Scale up an app in Azure](web-sites-scale.md).</span></span> <span data-ttu-id="384a7-114">**프리미엄** 계층을 사용하면 **표준** 계층보다 더 많은 매일 백업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="384a7-114">**Premium** tier allows a greater number of daily backups to be performed than **Standard** tier.</span></span>

<a name="PreviousBackup"></a>

## <a name="restore-an-app-from-an-existing-backup"></a><span data-ttu-id="384a7-115">기존 백업에서 앱 복원</span><span class="sxs-lookup"><span data-stu-id="384a7-115">Restore an app from an existing backup</span></span>
1. <span data-ttu-id="384a7-116">Azure Portal에서 앱의 **설정** 블레이드에서 **백업**을 클릭하여 **백업** 블레이드를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="384a7-116">On the **Settings** blade of your app in the Azure Portal, click **Backups** to display the **Backups** blade.</span></span> <span data-ttu-id="384a7-117">그런 다음 **복원**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="384a7-117">Then click **Restore**.</span></span>
   
    ![지금 복원 선택][ChooseRestoreNow]
2. <span data-ttu-id="384a7-119">**복원** 블레이드에서 먼저 백업 소스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="384a7-119">In the **Restore** blade, first select the backup source.</span></span>
   
    ![](./media/web-sites-restore/021ChooseSource1.png)
   
    <span data-ttu-id="384a7-120">**앱 백업** 옵션에는 현재 앱의 모든 기존 백업을 표시하며 백업 중 하나를 쉽게 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="384a7-120">The **App backup** option shows you all the existing backups of the current app, and you can easily select one.</span></span>
    <span data-ttu-id="384a7-121">**저장소** 옵션을 사용하면 구독의 기존 Azure 저장소 계정 및 컨테이너에서 백업 ZIP 파일을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="384a7-121">The **Storage** option lets you select any backup ZIP file from any existing Azure Storage account and container in your subscription.</span></span>
    <span data-ttu-id="384a7-122">다른 앱의 백업을 복원하려는 경우 **저장소** 옵션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="384a7-122">If you're trying to restore a backup of another app, use the **Storage** option.</span></span>
3. <span data-ttu-id="384a7-123">그런 다음 **복원 대상**에서 앱 복원 대상을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="384a7-123">Then, specify the destination for the app restore in **Restore destination**.</span></span>
   
    ![](./media/web-sites-restore/022ChooseDestination1.png)
   
   > [!WARNING]
   > <span data-ttu-id="384a7-124">**덮어쓰기**를 선택하면 현재 앱의 기존 데이터를 모두 지우고 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="384a7-124">If you choose **Overwrite**, all existing data in your current app is erased and overwritten.</span></span> <span data-ttu-id="384a7-125">**확인**을 클릭하기 전에 수행하려는 작업이 정확히 맞는지 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="384a7-125">Before you click **OK**, make sure that it is exactly what you want to do.</span></span>
   > 
   > 
   
    <span data-ttu-id="384a7-126">**기존 앱** 을 선택하여 같은 리소스 그룹에 있는 다른 앱으로 앱 백업을 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="384a7-126">You can select **Existing App** to restore the app backup to another app in the same resoure group.</span></span> <span data-ttu-id="384a7-127">이 옵션을 사용하려면 리소스 그룹에 미러링 데이터베이스가 앱 백업에 정의된 것으로 구성되어 있는 다른 앱이 이미 만들어져 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="384a7-127">Before you use this option, you should have already created another app in your resource group with mirroring database configuration to the one defined in the app backup.</span></span> <span data-ttu-id="384a7-128">**새** 앱을 만들어 콘텐츠를 복원할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="384a7-128">You can also Create a **New** app to restore your content to.</span></span>

4. <span data-ttu-id="384a7-129">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="384a7-129">Click **OK**.</span></span>

<a name="StorageAccount"></a>

## <a name="download-or-delete-a-backup-from-a-storage-account"></a><span data-ttu-id="384a7-130">저장소 계정에서 백업 다운로드 또는 삭제</span><span class="sxs-lookup"><span data-stu-id="384a7-130">Download or delete a backup from a storage account</span></span>
1. <span data-ttu-id="384a7-131">Azure Portal의 기본 **찾아보기** 블레이드에서 **저장소 계정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="384a7-131">From the main **Browse** blade of the Azure portal, select **Storage accounts**.</span></span> <span data-ttu-id="384a7-132">기존 저장소 계정 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="384a7-132">A list of your existing storage accounts is displayed.</span></span>
2. <span data-ttu-id="384a7-133">다운로드하거나 삭제하려는 백업이 포함된 저장소 계정을 선택합니다. 저장소 계정에 대한 블레이드가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="384a7-133">Select the storage account that contains the backup that you want to download or delete.The blade for the storage account is displayed.</span></span>
3. <span data-ttu-id="384a7-134">저장소 계정 블레이드에서 원하는 컨테이너를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="384a7-134">In the storage account blade, select the container you want</span></span>
   
    ![컨테이너 보기][ViewContainers]
4. <span data-ttu-id="384a7-136">다운로드 또는 삭제하려는 백업 파일을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="384a7-136">Select backup file you want to download or delete.</span></span>
   
    ![ViewContainers](./media/web-sites-restore/03ViewFiles.png)
5. <span data-ttu-id="384a7-138">수행하려는 작업에 따라 **다운로드** 또는 **삭제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="384a7-138">Click **Download** or **Delete** depending on what you want to do.</span></span>  

<a name="OperationLogs"></a>

## <a name="monitor-a-restore-operation"></a><span data-ttu-id="384a7-139">복원 작업 모니터링</span><span class="sxs-lookup"><span data-stu-id="384a7-139">Monitor a restore operation</span></span>
<span data-ttu-id="384a7-140">앱 복원 작업의 성공 또는 실패에 대한 자세한 내용을 보려면 Azure Portal의 **활동 로그** 블레이드로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="384a7-140">To see details about the success or failure of the app restore operation, navigate to the **Activity Log** blade in the Azure portal.</span></span>  
 

<span data-ttu-id="384a7-141">아래로 스크롤하여 원하는 복원 작업을 찾은 후 클릭하여 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="384a7-141">Scroll down to find the desired restore operation and click to select it.</span></span>

<span data-ttu-id="384a7-142">세부 정보 블레이드에서 복원 작업과 관련하여 사용 가능한 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="384a7-142">The details blade displays the available information related to the restore operation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="384a7-143">다음 단계</span><span class="sxs-lookup"><span data-stu-id="384a7-143">Next Steps</span></span>
<span data-ttu-id="384a7-144">REST API를 사용하여 App Service 앱을 백업하고 복원할 수 있습니다([REST를 사용하여 App Service 앱 백업 및 복원](websites-csm-backup.md)참조).</span><span class="sxs-lookup"><span data-stu-id="384a7-144">You can backup and restore App Service apps using REST API (see [Use REST to back up and restore App Service apps](websites-csm-backup.md)).</span></span>


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
