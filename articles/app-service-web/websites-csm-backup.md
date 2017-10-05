---
title: "REST를 사용하여 앱 서비스 앱 백업 및 복원"
description: "Azure 앱 서비스에서 RESTful API 호출을 사용하여 앱을 백업하고 복원하는 방법 알아보기"
services: app-service
documentationcenter: 
author: NKing92
manager: erikre
editor: 
ms.assetid: f94d0aea-edc1-43ab-9b51-ea7375859276
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2016
ms.author: nicking
ms.openlocfilehash: c1b8fc3be3af46279bf35bddbc82acf1827b9eb9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="use-rest-to-back-up-and-restore-app-service-apps"></a><span data-ttu-id="6bccd-103">REST를 사용하여 앱 서비스 앱 백업 및 복원</span><span class="sxs-lookup"><span data-stu-id="6bccd-103">Use REST to back up and restore App Service apps</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6bccd-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6bccd-104">PowerShell</span></span>](../app-service/app-service-powershell-backup.md)
> * [<span data-ttu-id="6bccd-105">REST API</span><span class="sxs-lookup"><span data-stu-id="6bccd-105">REST API</span></span>](websites-csm-backup.md)
> 
> 

<span data-ttu-id="6bccd-106">[Azure 서비스 앱](https://azure.microsoft.com/services/app-service/web/) 을 Azure 저장소에 blob로 백업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6bccd-106">[App Service apps](https://azure.microsoft.com/services/app-service/web/) can be backed up as blobs in Azure storage.</span></span> <span data-ttu-id="6bccd-107">또한 백업에 앱의 데이터베이스를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6bccd-107">The backup can also contain the app’s databases.</span></span> <span data-ttu-id="6bccd-108">앱이 실수로 삭제되거나 앱을 이전 버전으로 되돌려야 할 경우 이전 백업으로 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6bccd-108">If the app is ever accidentally deleted, or if the app needs to be reverted to a previous version, it can be restored from any previous backup.</span></span> <span data-ttu-id="6bccd-109">필요할 때 언제든지 백업할 수 있으며, 적당한 간격으로 백업을 예약할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6bccd-109">Backups can be done at any time on demand, or backups can be scheduled at suitable intervals.</span></span>

<span data-ttu-id="6bccd-110">이 문서에서는 RESTful API 요청을 사용하여 앱을 백업 및 복원하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="6bccd-110">This article explains how to backup and restore an app with RESTful API requests.</span></span> <span data-ttu-id="6bccd-111">Azure 포털을 통해 그래픽 방식으로 앱 백업을 만들고 관리하려면 [Azure 앱 서비스에서 웹앱 백업](web-sites-backup.md)</span><span class="sxs-lookup"><span data-stu-id="6bccd-111">If you would like to create and manage app backups graphically through the Azure portal, see [Back up a web app in Azure App Service](web-sites-backup.md)</span></span>

<a name="gettingstarted"></a>

## <a name="getting-started"></a><span data-ttu-id="6bccd-112">시작하기</span><span class="sxs-lookup"><span data-stu-id="6bccd-112">Getting Started</span></span>
<span data-ttu-id="6bccd-113">REST 요청을 보내려면 앱의 **이름**, **리소스 그룹** 및 **구독 id**를 알아야 합니다. 이 정보는 **Azure 포털** 의 [앱 서비스](https://portal.azure.com)블레이드에서 앱을 클릭하여 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6bccd-113">To send REST requests, you need to know your app’s **name**, **resource group**, and **subscription id**. This information can be found by clicking your app in the **App Service** blade of the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="6bccd-114">이 문서의 예에서는 웹 사이트 **backuprestoreapiexamples.azurewebsites.net**을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="6bccd-114">For the examples in this article, we are configuring the website **backuprestoreapiexamples.azurewebsites.net**.</span></span> <span data-ttu-id="6bccd-115">Default-Web-WestUS 리소스 그룹에 저장되며 ID가 00001111-2222-3333-4444-555566667777인 구독에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="6bccd-115">It is stored in the Default-Web-WestUS resource group and is running on a subscription with the ID 00001111-2222-3333-4444-555566667777.</span></span>

![샘플 웹 사이트 정보][SampleWebsiteInformation]

<a name="backup-restore-rest-api"></a>

## <a name="backup-and-restore-rest-api"></a><span data-ttu-id="6bccd-117">REST API 백업 및 복원</span><span class="sxs-lookup"><span data-stu-id="6bccd-117">Backup and restore REST API</span></span>
<span data-ttu-id="6bccd-118">이제 REST API를 사용하여 앱을 백업 및 복원하는 몇 가지 예를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="6bccd-118">We will now cover several examples of how to use the REST API to backup and restore an app.</span></span> <span data-ttu-id="6bccd-119">각 예제에는 URL 및 HTTP 요청 본문이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6bccd-119">Each example includes a URL and HTTP request body.</span></span> <span data-ttu-id="6bccd-120">샘플 URL에는 {subscription-id}처럼 중괄호로 묶인 자리 표시자가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6bccd-120">The sample URL contains placeholders wrapped in curly braces, such as {subscription-id}.</span></span> <span data-ttu-id="6bccd-121">이러한 자리 표시자를 앱의 해당 정보로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="6bccd-121">Replace the placeholders with the corresponding information for your app.</span></span> <span data-ttu-id="6bccd-122">예제 URL에 표시되는 각 자리 표시자에 대한 다음 설명을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6bccd-122">For reference, here is an explanation of each placeholder that appears in the example URLs.</span></span>

* <span data-ttu-id="6bccd-123">subscription-id – 앱이 포함된 Azure 구독의 ID</span><span class="sxs-lookup"><span data-stu-id="6bccd-123">subscription-id – ID of the Azure subscription containing the app</span></span>
* <span data-ttu-id="6bccd-124">resource-group-name – 앱이 포함된 리소스 그룹의 이름</span><span class="sxs-lookup"><span data-stu-id="6bccd-124">resource-group-name – Name of the resource group containing the app</span></span>
* <span data-ttu-id="6bccd-125">name – 앱의 이름</span><span class="sxs-lookup"><span data-stu-id="6bccd-125">name – Name of the app</span></span>
* <span data-ttu-id="6bccd-126">backup-id – 앱 백업의 ID</span><span class="sxs-lookup"><span data-stu-id="6bccd-126">backup-id – ID of the app backup</span></span>

<span data-ttu-id="6bccd-127">HTTP 요청에 포함할 수 있는 여러 선택적 매개 변수를 포함하여 API에 대한 전체 설명서는 [Azure 리소스 탐색기](https://resources.azure.com/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6bccd-127">For the complete documentation of the API, including several optional parameters that can be included in the HTTP request, see the [Azure Resource Explorer](https://resources.azure.com/).</span></span>

<a name="backup-on-demand"></a>

## <a name="backup-an-app-on-demand"></a><span data-ttu-id="6bccd-128">주문형 앱 백업</span><span class="sxs-lookup"><span data-stu-id="6bccd-128">Backup an app on demand</span></span>
<span data-ttu-id="6bccd-129">앱을 즉시 백업하려면 **POST** 요청을 **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backup/**으로 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="6bccd-129">To back up an app immediately, send a **POST** request to **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backup/**.</span></span>

<span data-ttu-id="6bccd-130">다음은 예제 웹 사이트를 사용한 URL의 모습입니다.</span><span class="sxs-lookup"><span data-stu-id="6bccd-130">Here is what the URL looks like using our example website.</span></span> <span data-ttu-id="6bccd-131">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backup/**</span><span class="sxs-lookup"><span data-stu-id="6bccd-131">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backup/**</span></span>

<span data-ttu-id="6bccd-132">요청 본문에 JSON 개체를 넣어서 백업을 저장하는 데 사용할 저장소 계정을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6bccd-132">Supply a JSON object in the body of your request to specify which storage account to use to store the backup.</span></span> <span data-ttu-id="6bccd-133">JSON 개체에 **storageAccountUrl**이라는 속성이 있어야 합니다. 이 속성에는 백업 Blob를 보관할 Azure Storage 컨테이너에 대한 쓰기 액세스 권한을 부여하는 [SAS URL](../storage/common/storage-dotnet-shared-access-signature-part-1.md)이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6bccd-133">The JSON object must have a property named **storageAccountUrl**, which holds a [SAS URL](../storage/common/storage-dotnet-shared-access-signature-part-1.md) granting write access to the Azure Storage container that holds the backup blob.</span></span> <span data-ttu-id="6bccd-134">데이터베이스를 백업하려면 백업할 데이터베이스의 이름, 유형 및 연결 문자열이 들어 있는 목록을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bccd-134">If you want to back up your databases, you must also supply a list containing the names, types, and connection strings of the databases to be backed up.</span></span>

```
{
    "properties":
    {
        "storageAccountUrl": “https://account.blob.core.windows.net/backups?sv=2015-02-21&sr=c&sig=DzlkBl7h32C8qCv%2BifdBRxE63r4iv0kZ9L7E0qP16sY%3D&se=2016-09-15T22%3A46%3A54Z&sp=rwdl”,
        “databases”: [
            {
                “databaseType”: “SqlAzure”,
                “name”: “MyDatabase1”,
                "connectionString": "<your database connection string>"
            }
        ]
    }
}
```

<span data-ttu-id="6bccd-135">요청이 수신되면 그 즉시 앱 백업이 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="6bccd-135">A backup of the app begins immediately when the request is received.</span></span> <span data-ttu-id="6bccd-136">백업 프로세스가 완료될 때까지 시간이 오래 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6bccd-136">The backup process may take a long time to complete.</span></span> <span data-ttu-id="6bccd-137">HTTP 응답에는 또 다른 요청에서 백업 상태를 보는 데 사용할 수 있는 ID가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6bccd-137">The HTTP response contains an ID that you can use in another request to see the status of the backup.</span></span> <span data-ttu-id="6bccd-138">다음은 백업 요청에 대한 HTTP 응답 본문의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="6bccd-138">Here is an example of the body of the HTTP response to our backup request.</span></span>

```
{
    "id": "/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples",
    "name": " backuprestoreapiexamples ",
    "type": "Microsoft.Web/sites",
    "location": "WestUS",
    "properties":    {
        "id": 1,
        "storageAccountUrl": “https://account.blob.core.windows.net/backups?sv=2015-02-21&sr=c&sig=DzlkBl7h32C8qCv%2BifdBRxE63r4iv0kZ9L7E0qP16sY%3D&se=2016-09-15T22%3A46%3A54Z&sp=rwdl”,
        "blobName": “backup_201509291825.zip”,
        "name": "backup_201509291825",
        "status": 4,
        "sizeInBytes": 0,
        "created": "2015-09-29T18:25:26.3992707Z",
        "log": null,
        "databases": [
            {
                "databaseType": "SqlAzure",
                "name": "MyDatabase1",
                "connectionString": "<your database connection string>"
            }
        ],
        "scheduled": false,
        "correlationId": "ea730f4d-dd06-4f7f-a090-9aa09k662h36",
    }
}
```

> [!NOTE]
> <span data-ttu-id="6bccd-139">오류 메시지는 HTTP 응답의 로그 속성에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6bccd-139">Error messages can be found in the log property of the HTTP response.</span></span>
> 
> 

<a name="schedule-automatic-backups"></a>

## <a name="schedule-automatic-backups"></a><span data-ttu-id="6bccd-140">자동 백업 예약</span><span class="sxs-lookup"><span data-stu-id="6bccd-140">Schedule automatic backups</span></span>
<span data-ttu-id="6bccd-141">주문형 앱 백업 외에도 자동으로 백업하도록 예약할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6bccd-141">In addition to backing up an app on demand, you can also schedule a backup to happen automatically.</span></span>

### <a name="set-up-a-new-automatic-backup-schedule"></a><span data-ttu-id="6bccd-142">새로운 자동 백업 일정 설정</span><span class="sxs-lookup"><span data-stu-id="6bccd-142">Set up a new automatic backup schedule</span></span>
<span data-ttu-id="6bccd-143">백업 일정을 설정하려면 **PUT** 요청을 **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/config/backup**으로 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="6bccd-143">To set up a backup schedule, send a **PUT** request to **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/config/backup**.</span></span>

<span data-ttu-id="6bccd-144">다음은 예제 웹 사이트의 URL 모습입니다.</span><span class="sxs-lookup"><span data-stu-id="6bccd-144">Here is what the URL looks like for our example website.</span></span> <span data-ttu-id="6bccd-145">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/config/backup**</span><span class="sxs-lookup"><span data-stu-id="6bccd-145">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/config/backup**</span></span>

<span data-ttu-id="6bccd-146">요청 본문에는 백업 구성을 지정하는 JSON 개체가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bccd-146">The request body must have a JSON object that specifies the backup configuration.</span></span> <span data-ttu-id="6bccd-147">다음은 필요한 매개 변수가 모두 포함된 예입니다.</span><span class="sxs-lookup"><span data-stu-id="6bccd-147">Here is an example with all the required parameters.</span></span>

```
{
    "location": "WestUS",
    "properties": // Represents an app restore request
    {
        "backupSchedule": { // Required for automatically scheduled backups
            "frequencyInterval": "7",
            "frequencyUnit": "Day",
            "keepAtLeastOneBackup": "True",
            "retentionPeriodInDays": "10",
        },
        "enabled": "True", // Must be set to true to enable automatic backups
        "name": “mysitebackup”,
        "storageAccountUrl": "https://account.blob.core.windows.net/backups?sv=2015-02-21&sr=c&sig=DzlkBl7h32C8qCv%2BifdBRxE63r4iv0kZ9L7E0qP16sY%3D&se=2016-09-15T22%3A46%3A54Z&sp=rwdl"
    }
}
```

<span data-ttu-id="6bccd-148">이 예에서는 7일마다 자동으로 앱을 백업하도록 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="6bccd-148">This example configures the app to be automatically backed up every seven days.</span></span> <span data-ttu-id="6bccd-149">매개 변수 **frequencyInterval** 및 **frequencyUnit**이 백업 빈도를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="6bccd-149">The parameters **frequencyInterval** and **frequencyUnit** together determine how often the backups happen.</span></span> <span data-ttu-id="6bccd-150">**frequencyUnit**에 유효한 값은 **시간** 및 **일**입니다.</span><span class="sxs-lookup"><span data-stu-id="6bccd-150">Valid values for **frequencyUnit** are **hour** and **day**.</span></span> <span data-ttu-id="6bccd-151">예를 들어 12시간마다 앱을 백업하려면 frequencyInterval을 12로, frequencyUnit을 시간으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="6bccd-151">For example, to back up an app every 12 hours, set frequencyInterval to 12 and frequencyUnit to hour.</span></span>

<span data-ttu-id="6bccd-152">기존 백업은 저장소 계정에서 자동으로 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="6bccd-152">Old backups are automatically removed from the storage account.</span></span> <span data-ttu-id="6bccd-153">**retentionPeriodInDays** 매개 변수를 설정하여 백업 보존 기간을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6bccd-153">You can control how old the backups can be by setting the **retentionPeriodInDays** parameter.</span></span> <span data-ttu-id="6bccd-154">백업 보존 기간에 관계없이 하나 이상의 백업을 항상 저장하려면 **keepAtLeastOneBackup** 을 true로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="6bccd-154">If you want to always have at least one backup saved, regardless of how old it is, set **keepAtLeastOneBackup** to true.</span></span>

### <a name="get-the-automatic-backup-schedule"></a><span data-ttu-id="6bccd-155">자동 백업 일정 가져오기</span><span class="sxs-lookup"><span data-stu-id="6bccd-155">Get the automatic backup schedule</span></span>
<span data-ttu-id="6bccd-156">앱의 백업 구성을 가져오려면 **POST** 요청을 **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/config/backup/list**로 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="6bccd-156">To get an app’s backup configuration, send a **POST** request to the URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/config/backup/list**.</span></span>

<span data-ttu-id="6bccd-157">예제 사이트의 URL은 **https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/config/backup/list**입니다.</span><span class="sxs-lookup"><span data-stu-id="6bccd-157">The URL for our example site is **https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/config/backup/list**.</span></span>

<a name="get-backup-status"></a>

## <a name="get-the-status-of-a-backup"></a><span data-ttu-id="6bccd-158">백업 상태 가져오기</span><span class="sxs-lookup"><span data-stu-id="6bccd-158">Get the status of a backup</span></span>
<span data-ttu-id="6bccd-159">앱의 크기에 따라 백업을 완료하는 데 다소 시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6bccd-159">Depending on how large the app is, a backup may take a while to complete.</span></span> <span data-ttu-id="6bccd-160">또한 백업이 실패하거나, 시간이 초과되거나, 부분적으로 성공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6bccd-160">Backups might also fail, time out, or partially succeed.</span></span> <span data-ttu-id="6bccd-161">모든 앱의 백업 상태를 보려면 **GET** 요청을 URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups**로 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="6bccd-161">To see the status of all an app’s backups, send a **GET** request to the URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups**.</span></span>

<span data-ttu-id="6bccd-162">특정 백업 상태를 보려면 GET 요청을 URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups/{backup-id}**로 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="6bccd-162">To see the status of a specific backup, send a GET request to the URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups/{backup-id}**.</span></span>

<span data-ttu-id="6bccd-163">다음은 예제 웹 사이트의 URL 모습입니다.</span><span class="sxs-lookup"><span data-stu-id="6bccd-163">Here is what the URL looks like for our example website.</span></span> <span data-ttu-id="6bccd-164">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1**</span><span class="sxs-lookup"><span data-stu-id="6bccd-164">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1**</span></span>

<span data-ttu-id="6bccd-165">응답 본문에는 이 예와 비슷한 JSON 개체가 들어 있을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6bccd-165">The response body contains a JSON object similar to this example.</span></span>

```
{
    "properties":  {
        "id": 1,
        "storageAccountUrl": "https://account.blob.core.windows.net/backups?sv=2015-02-21&sr=c&sig=DzlkBl7h32C8qCv%2BifdBRxE63r4iv0kZ9L7E0qP16sY%3D&se=2016-09-15T22%3A46%3A54Z&sp=rwdl",
        "blobName": "backup_201509291734.zip",
        "name": "backup_201509291734",
        "status": 2,
        "sizeInBytes": 151973,
        "created": "2015-09-29T17:34:57.2091605",
        "scheduled": false,
        "lastRestoreTimeStamp": null,
        "finishedTimeStamp": "2015-09-29T17:35:11.3293602",
        "correlationId": "2379fc13-418a-4b9c-920d-d06e73c5028d",
        "websiteSizeInBytes": 209920
    }
}
```

<span data-ttu-id="6bccd-166">백업 상태가 열거 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="6bccd-166">The status of a backup is an enumerated type.</span></span> <span data-ttu-id="6bccd-167">다음과 같은 상태가 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="6bccd-167">Here is every possible state.</span></span>

* <span data-ttu-id="6bccd-168">0 – InProgress: 백업이 시작되었지만 아직 완료되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="6bccd-168">0 – InProgress: The backup has been started but has not yet completed.</span></span>
* <span data-ttu-id="6bccd-169">1 – Failed: 백업이 실패했습니다.</span><span class="sxs-lookup"><span data-stu-id="6bccd-169">1 – Failed: The backup was unsuccessful.</span></span>
* <span data-ttu-id="6bccd-170">2 – Succeeded: 백업이 완료되었습니다.</span><span class="sxs-lookup"><span data-stu-id="6bccd-170">2 – Succeeded: The backup completed successfully.</span></span>
* <span data-ttu-id="6bccd-171">3 – TimedOut: 백업이 시간 내에 완료되지 않아 취소되었습니다.</span><span class="sxs-lookup"><span data-stu-id="6bccd-171">3 – TimedOut: The backup did not finish in time and was canceled.</span></span>
* <span data-ttu-id="6bccd-172">4 – Created: 대기열에 백업 요청이 생성되었지만 아직 시작되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="6bccd-172">4 – Created: The backup request is queued but has not been started.</span></span>
* <span data-ttu-id="6bccd-173">5 – Skipped: 일정에서 너무 많은 백업을 트리거하여 백업이 진행되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="6bccd-173">5 – Skipped: The backup did not proceed due to a schedule triggering too many backups.</span></span>
* <span data-ttu-id="6bccd-174">6 – PartiallySucceeded: 백업을 성공했지만 일부 파일을 읽을 수 없어 백업하지 못했습니다.</span><span class="sxs-lookup"><span data-stu-id="6bccd-174">6 – PartiallySucceeded: The backup succeeded, but some files were not backed up because they could not be read.</span></span> <span data-ttu-id="6bccd-175">이 문제는 일반적으로 파일에 배타적 잠금이 설정된 경우에 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="6bccd-175">This usually happens because an exclusive lock was placed on the files.</span></span>
* <span data-ttu-id="6bccd-176">7 – DeleteInProgress: 백업을 삭제하라는 요청이 있었지만 아직 삭제되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="6bccd-176">7 – DeleteInProgress: The backup has been requested to be deleted, but has not yet been deleted.</span></span>
* <span data-ttu-id="6bccd-177">8 – DeleteFailed: 백업을 삭제하지 못했습니다.</span><span class="sxs-lookup"><span data-stu-id="6bccd-177">8 – DeleteFailed: The backup could not be deleted.</span></span> <span data-ttu-id="6bccd-178">백업을 만드는 데 사용된 SAS URL이 만료된 것이 원인일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6bccd-178">This might happen because the SAS URL that was used to create the backup has expired.</span></span>
* <span data-ttu-id="6bccd-179">9 – Deleted: 백업이 삭제되었습니다.</span><span class="sxs-lookup"><span data-stu-id="6bccd-179">9 – Deleted: The backup was deleted successfully.</span></span>

<a name="restore-app"></a>

## <a name="restore-an-app-from-a-backup"></a><span data-ttu-id="6bccd-180">백업으로 앱 복원</span><span class="sxs-lookup"><span data-stu-id="6bccd-180">Restore an app from a backup</span></span>
<span data-ttu-id="6bccd-181">앱이 삭제되었거나 앱을 이전 버전으로 되돌리고 싶은 경우 백업으로 앱을 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6bccd-181">If your app has been deleted, or if you want to revert your app to a previous version, you can restore the app from a backup.</span></span> <span data-ttu-id="6bccd-182">복원을 호출하려면 **POST** 요청을 URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups/{backup-id}/restore**로 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="6bccd-182">To invoke a restore, send a **POST** request to the URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups/{backup-id}/restore**.</span></span>

<span data-ttu-id="6bccd-183">다음은 예제 웹 사이트의 URL 모습입니다.</span><span class="sxs-lookup"><span data-stu-id="6bccd-183">Here is what the URL looks like for our example website.</span></span> <span data-ttu-id="6bccd-184">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1/restore**</span><span class="sxs-lookup"><span data-stu-id="6bccd-184">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1/restore**</span></span>

<span data-ttu-id="6bccd-185">요청 본문에서 복원 작업의 속성이 포함된 JSON 개체를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="6bccd-185">In the request body, send a JSON object that contains the properties for the restore operation.</span></span> <span data-ttu-id="6bccd-186">다음은 필요한 속성이 모두 포함된 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="6bccd-186">Here is an example containing all required properties:</span></span>

```
{
    "location": "WestUS",
    "properties":
    {
        "blobName": "backup_201509280431.zip",
        "databases": [ // Not required unless you’re restoring databases
            {
                “databaseType”: “SqlAzure”,
                “name”: “MyDatabase1”
        }],
        "overwrite": "true",
        "storageAccountUrl": "https://account.blob.core.windows.net/backups?sv=2015-02-21&sr=c&sig=DzlkBl7h32C8qCv%2BifdBRxE63r4iv0kZ9L7E0qP16sY%3D&se=2016-09-15T22%3A46%3A54Z&sp=rwdl" // SAS URL to storage container containing your website backup
    }
}
```

### <a name="restore-to-a-new-app"></a><span data-ttu-id="6bccd-187">새 앱으로 복원</span><span class="sxs-lookup"><span data-stu-id="6bccd-187">Restore to a new app</span></span>
<span data-ttu-id="6bccd-188">백업을 복원할 때 기존 앱을 덮어쓰지 않고 새 앱을 만들려는 경우가 종종 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6bccd-188">Sometimes you might want to create a new app when you restore a backup, instead of overwriting an already existing app.</span></span> <span data-ttu-id="6bccd-189">이렇게 하려면 만들고 싶은 새 앱을 가리키도록 요청 URL을 변경하고, JSON의 **덮어쓰기** 속성을 **false**로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="6bccd-189">To do this, change the request URL to point to the new app you want to create, and change the **overwrite** property in the JSON to **false**.</span></span>

<a name="delete-app-backup"></a>

## <a name="delete-an-app-backup"></a><span data-ttu-id="6bccd-190">앱 백업 삭제</span><span class="sxs-lookup"><span data-stu-id="6bccd-190">Delete an app backup</span></span>
<span data-ttu-id="6bccd-191">백업을 삭제하려면 **DELETE** 요청을 URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups/{backup-id}**로 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="6bccd-191">If you would like to delete a backup, send a **DELETE** request to the URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups/{backup-id}**.</span></span>

<span data-ttu-id="6bccd-192">다음은 예제 웹 사이트의 URL 모습입니다.</span><span class="sxs-lookup"><span data-stu-id="6bccd-192">Here is what the URL looks like for our example website.</span></span> <span data-ttu-id="6bccd-193">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1**</span><span class="sxs-lookup"><span data-stu-id="6bccd-193">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1**</span></span>

<a name="manage-sas-url"></a>

## <a name="manage-a-backups-sas-url"></a><span data-ttu-id="6bccd-194">백업의 SAS URL 관리</span><span class="sxs-lookup"><span data-stu-id="6bccd-194">Manage a backup’s SAS URL</span></span>
<span data-ttu-id="6bccd-195">Azure 앱 서비스에서는 백업을 만들 때 제공된 SAS URL을 사용하여 Azure 저장소에서 백업을 삭제하려고 시도할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6bccd-195">Azure App Service will attempt to delete your backup from Azure Storage using the SAS URL that was provided when the backup was created.</span></span> <span data-ttu-id="6bccd-196">이 SAS URL이 더 이상 유효하지 않으면 REST API를 통해 백업을 삭제할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6bccd-196">If this SAS URL is no longer valid, the backup cannot be deleted through the REST API.</span></span> <span data-ttu-id="6bccd-197">그러나 **POST** 요청을 URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups/{backup-id}/list**로 전송하여 백업과 연결된 SAS URL을 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6bccd-197">However, you can update the SAS URL associated with a backup by sending a **POST** request to the URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups/{backup-id}/list**.</span></span>

<span data-ttu-id="6bccd-198">다음은 예제 웹 사이트의 URL 모습입니다.</span><span class="sxs-lookup"><span data-stu-id="6bccd-198">Here is what the URL looks like for our example website.</span></span> <span data-ttu-id="6bccd-199">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1/list**</span><span class="sxs-lookup"><span data-stu-id="6bccd-199">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1/list**</span></span>

<span data-ttu-id="6bccd-200">요청 본문에서 새 SAS URL이 포함된 JSON 개체를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="6bccd-200">In the request body, send a JSON object that contains the new SAS URL.</span></span> <span data-ttu-id="6bccd-201">다음은 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="6bccd-201">Here is an example.</span></span>

```
{
    "properties":
    {
        "storageAccountUrl": "https://account.blob.core.windows.net/backups?sv=2015-02-21&sr=c&sig=DzlkBl7h32C8qCv%2BifdBRxE63r4iv0kZ9L7E0qP16sY%3D&se=2016-09-15T22%3A46%3A54Z&sp=rwdl"
    }
}
```

> [!NOTE]
> <span data-ttu-id="6bccd-202">보안을 위해 특정 백업에 대한 GET 요청을 보낼 때 백업과 연결된 SAS URL이 반환되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6bccd-202">For security reasons, the SAS URL associated with a backup is not returned when sending a GET request for a specific backup.</span></span> <span data-ttu-id="6bccd-203">백업과 연결된 SAS URL을 보고 싶으면 위와 동일한 URL에 POST 요청을 보내고</span><span class="sxs-lookup"><span data-stu-id="6bccd-203">If you want to view the SAS URL associated with a backup, send a POST request to the same URL above.</span></span> <span data-ttu-id="6bccd-204">요청 본문에 빈 JSON 개체를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="6bccd-204">Include an empty JSON object in the request body.</span></span> <span data-ttu-id="6bccd-205">서버의 응답에 SAS URL을 포함하여 해당 백업의 모든 정보가 들어 있을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6bccd-205">The response from the server contains all of that backup’s information, including its SAS URL.</span></span>
> 
> 

<!-- IMAGES -->
[SampleWebsiteInformation]: ./media/websites-csm-backup/01siteconfig.png
