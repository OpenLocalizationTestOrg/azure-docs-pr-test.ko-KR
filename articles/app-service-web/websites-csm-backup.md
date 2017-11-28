---
title: "aaaUse tooback를 놓고 앱 서비스 앱 복원"
description: "RESTful API toouse tooback 호출 하는 방법에 대해 알아봅니다 및 Azure 앱 서비스의 응용 프로그램 복원"
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
ms.openlocfilehash: f77bdfc7de1626d04d8d0c0e8979231ae1ced81a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-rest-tooback-up-and-restore-app-service-apps"></a><span data-ttu-id="2c02e-103">앱 서비스 앱을 복원 및 REST tooback 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="2c02e-103">Use REST tooback up and restore App Service apps</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2c02e-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2c02e-104">PowerShell</span></span>](../app-service/app-service-powershell-backup.md)
> * [<span data-ttu-id="2c02e-105">REST API</span><span class="sxs-lookup"><span data-stu-id="2c02e-105">REST API</span></span>](websites-csm-backup.md)
> 
> 

<span data-ttu-id="2c02e-106">[Azure 서비스 앱](https://azure.microsoft.com/services/app-service/web/) 을 Azure 저장소에 blob로 백업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c02e-106">[App Service apps](https://azure.microsoft.com/services/app-service/web/) can be backed up as blobs in Azure storage.</span></span> <span data-ttu-id="2c02e-107">hello 백업 hello 응용 프로그램의 데이터베이스를 포함할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c02e-107">hello backup can also contain hello app’s databases.</span></span> <span data-ttu-id="2c02e-108">Hello 앱도 실수로 삭제 된, 또는 hello 앱 요구 toobe tooa 이전 버전 되돌려 진 경우에 모든 이전 백업에서 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c02e-108">If hello app is ever accidentally deleted, or if hello app needs toobe reverted tooa previous version, it can be restored from any previous backup.</span></span> <span data-ttu-id="2c02e-109">필요할 때 언제든지 백업할 수 있으며, 적당한 간격으로 백업을 예약할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c02e-109">Backups can be done at any time on demand, or backups can be scheduled at suitable intervals.</span></span>

<span data-ttu-id="2c02e-110">이 문서에서는 toobackup 및 복원 RESTful API를 사용 하 여 앱 요청 하는 방식에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c02e-110">This article explains how toobackup and restore an app with RESTful API requests.</span></span> <span data-ttu-id="2c02e-111">Toocreate 같은 hello Azure 포털을 통해 그래픽으로 응용 프로그램 백업 관리는 경우 참조 [Azure 앱 서비스의 웹 앱 백업](web-sites-backup.md)</span><span class="sxs-lookup"><span data-stu-id="2c02e-111">If you would like toocreate and manage app backups graphically through hello Azure portal, see [Back up a web app in Azure App Service](web-sites-backup.md)</span></span>

<a name="gettingstarted"></a>

## <a name="getting-started"></a><span data-ttu-id="2c02e-112">시작하기</span><span class="sxs-lookup"><span data-stu-id="2c02e-112">Getting Started</span></span>
<span data-ttu-id="2c02e-113">toosend REST 요청, 응용 프로그램의 tooknow 필요한 **이름**, **리소스 그룹**, 및 **구독 id**합니다. Hello에서 응용 프로그램을 클릭 하 여이 정보를 찾을 수 **앱 서비스** hello의 블레이드에서 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="2c02e-113">toosend REST requests, you need tooknow your app’s **name**, **resource group**, and **subscription id**. This information can be found by clicking your app in hello **App Service** blade of hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="2c02e-114">이 문서의 예제 hello에 대 한 구성 하는 hello 웹 사이트 **backuprestoreapiexamples.azurewebsites.net**합니다.</span><span class="sxs-lookup"><span data-stu-id="2c02e-114">For hello examples in this article, we are configuring hello website **backuprestoreapiexamples.azurewebsites.net**.</span></span> <span data-ttu-id="2c02e-115">Hello WestUS-Web-기본 리소스 그룹에 저장 하 고 hello ID 00001111-2222-3333-4444-555566667777 인 구독에서 실행 되 고 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c02e-115">It is stored in hello Default-Web-WestUS resource group and is running on a subscription with hello ID 00001111-2222-3333-4444-555566667777.</span></span>

![샘플 웹 사이트 정보][SampleWebsiteInformation]

<a name="backup-restore-rest-api"></a>

## <a name="backup-and-restore-rest-api"></a><span data-ttu-id="2c02e-117">REST API 백업 및 복원</span><span class="sxs-lookup"><span data-stu-id="2c02e-117">Backup and restore REST API</span></span>
<span data-ttu-id="2c02e-118">이제 여러 가지 예 toouse REST API toobackup hello 하 고 응용 프로그램을 복원 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c02e-118">We will now cover several examples of how toouse hello REST API toobackup and restore an app.</span></span> <span data-ttu-id="2c02e-119">각 예제에는 URL 및 HTTP 요청 본문이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c02e-119">Each example includes a URL and HTTP request body.</span></span> <span data-ttu-id="2c02e-120">hello 샘플 URL {구독 id} 등의 중괄호에 래핑된 자리 표시자를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c02e-120">hello sample URL contains placeholders wrapped in curly braces, such as {subscription-id}.</span></span> <span data-ttu-id="2c02e-121">앱에 대 한 해당 정보를 hello hello 자리 표시자를 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="2c02e-121">Replace hello placeholders with hello corresponding information for your app.</span></span> <span data-ttu-id="2c02e-122">참조용으로 hello Url 예에에서 표시 되는 각 자리 표시자에 대 한 설명을 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2c02e-122">For reference, here is an explanation of each placeholder that appears in hello example URLs.</span></span>

* <span data-ttu-id="2c02e-123">구독 id-hello Azure 구독 포함 hello 응용 프로그램의 ID</span><span class="sxs-lookup"><span data-stu-id="2c02e-123">subscription-id – ID of hello Azure subscription containing hello app</span></span>
* <span data-ttu-id="2c02e-124">리소스 그룹 이름-hello 리소스 그룹 포함 hello 앱의 이름</span><span class="sxs-lookup"><span data-stu-id="2c02e-124">resource-group-name – Name of hello resource group containing hello app</span></span>
* <span data-ttu-id="2c02e-125">이름-hello 응용 프로그램의 이름</span><span class="sxs-lookup"><span data-stu-id="2c02e-125">name – Name of hello app</span></span>
* <span data-ttu-id="2c02e-126">백업-id-ID hello 응용 프로그램 백업</span><span class="sxs-lookup"><span data-stu-id="2c02e-126">backup-id – ID of hello app backup</span></span>

<span data-ttu-id="2c02e-127">Hello hello API의 전체 설명서를 hello 참조 hello HTTP 요청에 포함 될 수 있는 여러 가지 선택적 매개 변수를 포함 하 여 [Azure 리소스 탐색기](https://resources.azure.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="2c02e-127">For hello complete documentation of hello API, including several optional parameters that can be included in hello HTTP request, see hello [Azure Resource Explorer](https://resources.azure.com/).</span></span>

<a name="backup-on-demand"></a>

## <a name="backup-an-app-on-demand"></a><span data-ttu-id="2c02e-128">주문형 앱 백업</span><span class="sxs-lookup"><span data-stu-id="2c02e-128">Backup an app on demand</span></span>
<span data-ttu-id="2c02e-129">응용 프로그램을 tooback 즉시 보냅니다는 **POST** 너무 요청**https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/ 백업 /**합니다.</span><span class="sxs-lookup"><span data-stu-id="2c02e-129">tooback up an app immediately, send a **POST** request too**https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backup/**.</span></span>

<span data-ttu-id="2c02e-130">다음은 예제 웹 사이트를 사용 하 여 모양 hello URL입니다.</span><span class="sxs-lookup"><span data-stu-id="2c02e-130">Here is what hello URL looks like using our example website.</span></span> <span data-ttu-id="2c02e-131">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backup/**</span><span class="sxs-lookup"><span data-stu-id="2c02e-131">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backup/**</span></span>

<span data-ttu-id="2c02e-132">저장소 계정 toouse toostore hello 백업 하 여 요청 toospecify의 hello 본문에서 JSON 개체를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c02e-132">Supply a JSON object in hello body of your request toospecify which storage account toouse toostore hello backup.</span></span> <span data-ttu-id="2c02e-133">hello JSON 개체 라는 속성이 있어야 합니다. **storageAccountUrl**를 보유 하는 [SAS URL](../storage/common/storage-dotnet-shared-access-signature-part-1.md) 쓰기 액세스 toohello Azure 저장소 컨테이너 hello 백업 blob을 포함 하는 권한을 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c02e-133">hello JSON object must have a property named **storageAccountUrl**, which holds a [SAS URL](../storage/common/storage-dotnet-shared-access-signature-part-1.md) granting write access toohello Azure Storage container that holds hello backup blob.</span></span> <span data-ttu-id="2c02e-134">데이터베이스를 tooback 하려는 경우 hello 이름, 유형 및 백업 hello 데이터베이스 toobe의 연결 문자열을 포함 하는 목록도 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c02e-134">If you want tooback up your databases, you must also supply a list containing hello names, types, and connection strings of hello databases toobe backed up.</span></span>

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

<span data-ttu-id="2c02e-135">Hello 응용 프로그램의 백업을 즉시 hello 요청을 받으면 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2c02e-135">A backup of hello app begins immediately when hello request is received.</span></span> <span data-ttu-id="2c02e-136">hello 백업 프로세스는 시간이 오래 toocomplete를 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c02e-136">hello backup process may take a long time toocomplete.</span></span> <span data-ttu-id="2c02e-137">HTTP 응답 hello 다른 요청 toosee hello hello 백업 상태에서 사용할 수 있는 ID를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c02e-137">hello HTTP response contains an ID that you can use in another request toosee hello status of hello backup.</span></span> <span data-ttu-id="2c02e-138">Hello hello HTTP 응답 tooour 백업 요청 본문의 예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2c02e-138">Here is an example of hello body of hello HTTP response tooour backup request.</span></span>

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
> <span data-ttu-id="2c02e-139">오류 메시지의 HTTP 응답 hello hello log 속성에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c02e-139">Error messages can be found in hello log property of hello HTTP response.</span></span>
> 
> 

<a name="schedule-automatic-backups"></a>

## <a name="schedule-automatic-backups"></a><span data-ttu-id="2c02e-140">자동 백업 예약</span><span class="sxs-lookup"><span data-stu-id="2c02e-140">Schedule automatic backups</span></span>
<span data-ttu-id="2c02e-141">필요에 따라 앱을 추가 toobacking, 백업 toohappen을 예약할 자동으로 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c02e-141">In addition toobacking up an app on demand, you can also schedule a backup toohappen automatically.</span></span>

### <a name="set-up-a-new-automatic-backup-schedule"></a><span data-ttu-id="2c02e-142">새로운 자동 백업 일정 설정</span><span class="sxs-lookup"><span data-stu-id="2c02e-142">Set up a new automatic backup schedule</span></span>
<span data-ttu-id="2c02e-143">백업 일정을 tooset 보내기는 **배치** 너무 요청**https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/config 백업/**합니다.</span><span class="sxs-lookup"><span data-stu-id="2c02e-143">tooset up a backup schedule, send a **PUT** request too**https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/config/backup**.</span></span>

<span data-ttu-id="2c02e-144">예제 웹 사이트에 대 한 hello URL 모양을 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2c02e-144">Here is what hello URL looks like for our example website.</span></span> <span data-ttu-id="2c02e-145">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/config/backup**</span><span class="sxs-lookup"><span data-stu-id="2c02e-145">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/config/backup**</span></span>

<span data-ttu-id="2c02e-146">hello 요청 본문에는 hello 백업 구성을 지정 하는 JSON 개체가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c02e-146">hello request body must have a JSON object that specifies hello backup configuration.</span></span> <span data-ttu-id="2c02e-147">모든 필요한 hello 매개 변수가 있는 예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2c02e-147">Here is an example with all hello required parameters.</span></span>

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
        "enabled": "True", // Must be set tootrue tooenable automatic backups
        "name": “mysitebackup”,
        "storageAccountUrl": "https://account.blob.core.windows.net/backups?sv=2015-02-21&sr=c&sig=DzlkBl7h32C8qCv%2BifdBRxE63r4iv0kZ9L7E0qP16sY%3D&se=2016-09-15T22%3A46%3A54Z&sp=rwdl"
    }
}
```

<span data-ttu-id="2c02e-148">이 예제에서는 구성 hello 앱 toobe 7 일 마다 자동으로 백업 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c02e-148">This example configures hello app toobe automatically backed up every seven days.</span></span> <span data-ttu-id="2c02e-149">매개 변수를 hello **frequencyInterval** 및 **frequencyUnit** 얼마나 자주 hello 백업을 수행할를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c02e-149">hello parameters **frequencyInterval** and **frequencyUnit** together determine how often hello backups happen.</span></span> <span data-ttu-id="2c02e-150">**frequencyUnit**에 유효한 값은 **시간** 및 **일**입니다.</span><span class="sxs-lookup"><span data-stu-id="2c02e-150">Valid values for **frequencyUnit** are **hour** and **day**.</span></span> <span data-ttu-id="2c02e-151">예를 들어, 12 시간 마다 앱을 tooback frequencyInterval too12 및 frequencyUnit toohour를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c02e-151">For example, tooback up an app every 12 hours, set frequencyInterval too12 and frequencyUnit toohour.</span></span>

<span data-ttu-id="2c02e-152">오래 된 백업 hello 저장소 계정에서 자동으로 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2c02e-152">Old backups are automatically removed from hello storage account.</span></span> <span data-ttu-id="2c02e-153">오래 된 hello hello 설정 하 여 백업 수를 제어할 수 있습니다 **retentionPeriodInDays** 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="2c02e-153">You can control how old hello backups can be by setting hello **retentionPeriodInDays** parameter.</span></span> <span data-ttu-id="2c02e-154">Tooalways 백업이 하나 이상 설정 되어, 오래 된 정도 관계 없이 저장 하려면 **keepAtLeastOneBackup** tootrue 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c02e-154">If you want tooalways have at least one backup saved, regardless of how old it is, set **keepAtLeastOneBackup** tootrue.</span></span>

### <a name="get-hello-automatic-backup-schedule"></a><span data-ttu-id="2c02e-155">Hello 자동 백업 일정 가져오기</span><span class="sxs-lookup"><span data-stu-id="2c02e-155">Get hello automatic backup schedule</span></span>
<span data-ttu-id="2c02e-156">tooget 응용 프로그램의 백업 구성, 전송 된 **POST** 요청 toohello URL **https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/ 사이트 / {name} / config/백업/목록**합니다.</span><span class="sxs-lookup"><span data-stu-id="2c02e-156">tooget an app’s backup configuration, send a **POST** request toohello URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/config/backup/list**.</span></span>

<span data-ttu-id="2c02e-157">이 예제에서는 사이트에 대 한 hello URL은 **https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/config/backup/list**합니다.</span><span class="sxs-lookup"><span data-stu-id="2c02e-157">hello URL for our example site is **https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/config/backup/list**.</span></span>

<a name="get-backup-status"></a>

## <a name="get-hello-status-of-a-backup"></a><span data-ttu-id="2c02e-158">백업 hello 상태를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="2c02e-158">Get hello status of a backup</span></span>
<span data-ttu-id="2c02e-159">Hello 앱 크기에 따라 이면 백업에는 시간이 걸릴 수 toocomplete 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c02e-159">Depending on how large hello app is, a backup may take a while toocomplete.</span></span> <span data-ttu-id="2c02e-160">또한 백업이 실패하거나, 시간이 초과되거나, 부분적으로 성공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c02e-160">Backups might also fail, time out, or partially succeed.</span></span> <span data-ttu-id="2c02e-161">모든 응용 프로그램의 백업의 toosee hello 상태 보내기는 **가져오기** 요청 toohello URL **https://management.azure.com/subscriptions/ {구독 id} {리소스 그룹 이름} /resourceGroups/ /providers/ Microsoft.Web/sites/{name}/backups**합니다.</span><span class="sxs-lookup"><span data-stu-id="2c02e-161">toosee hello status of all an app’s backups, send a **GET** request toohello URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups**.</span></span>

<span data-ttu-id="2c02e-162">특정 백업 toosee hello 상태 GET 요청 toohello URL 보내기 **https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups/ { 백업-id}**합니다.</span><span class="sxs-lookup"><span data-stu-id="2c02e-162">toosee hello status of a specific backup, send a GET request toohello URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups/{backup-id}**.</span></span>

<span data-ttu-id="2c02e-163">예제 웹 사이트에 대 한 hello URL 모양을 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2c02e-163">Here is what hello URL looks like for our example website.</span></span> <span data-ttu-id="2c02e-164">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1**</span><span class="sxs-lookup"><span data-stu-id="2c02e-164">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1**</span></span>

<span data-ttu-id="2c02e-165">hello 응답 본문에는 JSON 개체 유사한 toothis 예 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c02e-165">hello response body contains a JSON object similar toothis example.</span></span>

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

<span data-ttu-id="2c02e-166">hello 한 백업 상태는 열거 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="2c02e-166">hello status of a backup is an enumerated type.</span></span> <span data-ttu-id="2c02e-167">다음과 같은 상태가 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="2c02e-167">Here is every possible state.</span></span>

* <span data-ttu-id="2c02e-168">0 – InProgress: hello 백업 시작 되었지만 아직 완료 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="2c02e-168">0 – InProgress: hello backup has been started but has not yet completed.</span></span>
* <span data-ttu-id="2c02e-169">1 – 실패: hello 백업 하지 못했습니다.</span><span class="sxs-lookup"><span data-stu-id="2c02e-169">1 – Failed: hello backup was unsuccessful.</span></span>
* <span data-ttu-id="2c02e-170">2 – 성공된: hello 백업이 성공적으로 완료 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="2c02e-170">2 – Succeeded: hello backup completed successfully.</span></span>
* <span data-ttu-id="2c02e-171">3 – TimedOut: hello 백업 시간에 마치지 못함 및 취소 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="2c02e-171">3 – TimedOut: hello backup did not finish in time and was canceled.</span></span>
* <span data-ttu-id="2c02e-172">4 –: hello 백업 요청 큐에 대기 만들어지지만 시작 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="2c02e-172">4 – Created: hello backup request is queued but has not been started.</span></span>
* <span data-ttu-id="2c02e-173">5 – 생략: hello 백업을 계속할 수 없습니다 인해 너무 많은 백업을 트리거하지 tooa 일정.</span><span class="sxs-lookup"><span data-stu-id="2c02e-173">5 – Skipped: hello backup did not proceed due tooa schedule triggering too many backups.</span></span>
* <span data-ttu-id="2c02e-174">6-PartiallySucceeded: hello 백업 성공 했지만 일부 파일이 백업 되지 않은 이러한를 읽을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2c02e-174">6 – PartiallySucceeded: hello backup succeeded, but some files were not backed up because they could not be read.</span></span> <span data-ttu-id="2c02e-175">이 문제는 일반적으로 배타적 잠금이 hello 파일에 배치 하기 때문에 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c02e-175">This usually happens because an exclusive lock was placed on hello files.</span></span>
* <span data-ttu-id="2c02e-176">7-DeleteInProgress: hello 백업을 삭제 하는 요청 된 toobe 되었지만 아직 삭제 되지 않은 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c02e-176">7 – DeleteInProgress: hello backup has been requested toobe deleted, but has not yet been deleted.</span></span>
* <span data-ttu-id="2c02e-177">8-삭제 실패: hello 백업을 삭제할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2c02e-177">8 – DeleteFailed: hello backup could not be deleted.</span></span> <span data-ttu-id="2c02e-178">이 SAS URL을 사용 하는 toocreate hello 백업 hello 만료 되었기 때문에 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c02e-178">This might happen because hello SAS URL that was used toocreate hello backup has expired.</span></span>
* <span data-ttu-id="2c02e-179">9-삭제 됨: hello 백업 삭제 했습니다.</span><span class="sxs-lookup"><span data-stu-id="2c02e-179">9 – Deleted: hello backup was deleted successfully.</span></span>

<a name="restore-app"></a>

## <a name="restore-an-app-from-a-backup"></a><span data-ttu-id="2c02e-180">백업으로 앱 복원</span><span class="sxs-lookup"><span data-stu-id="2c02e-180">Restore an app from a backup</span></span>
<span data-ttu-id="2c02e-181">응용 프로그램 삭제 되었거나 또는 toorevert 응용 프로그램 tooa 이전 버전을 사용할 경우 백업에서 hello 응용 프로그램을 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c02e-181">If your app has been deleted, or if you want toorevert your app tooa previous version, you can restore hello app from a backup.</span></span> <span data-ttu-id="2c02e-182">tooinvoke 복원 하는 보내기는 **POST** 요청 toohello URL **https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/ 백업 / {백업 id} / 복원**합니다.</span><span class="sxs-lookup"><span data-stu-id="2c02e-182">tooinvoke a restore, send a **POST** request toohello URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups/{backup-id}/restore**.</span></span>

<span data-ttu-id="2c02e-183">예제 웹 사이트에 대 한 hello URL 모양을 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2c02e-183">Here is what hello URL looks like for our example website.</span></span> <span data-ttu-id="2c02e-184">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1/restore**</span><span class="sxs-lookup"><span data-stu-id="2c02e-184">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1/restore**</span></span>

<span data-ttu-id="2c02e-185">Hello 요청 본문에 hello 복원 작업에 대 한 hello 속성을 포함 하는 JSON 개체를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="2c02e-185">In hello request body, send a JSON object that contains hello properties for hello restore operation.</span></span> <span data-ttu-id="2c02e-186">다음은 필요한 속성이 모두 포함된 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="2c02e-186">Here is an example containing all required properties:</span></span>

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
        "storageAccountUrl": "https://account.blob.core.windows.net/backups?sv=2015-02-21&sr=c&sig=DzlkBl7h32C8qCv%2BifdBRxE63r4iv0kZ9L7E0qP16sY%3D&se=2016-09-15T22%3A46%3A54Z&sp=rwdl" // SAS URL toostorage container containing your website backup
    }
}
```

### <a name="restore-tooa-new-app"></a><span data-ttu-id="2c02e-187">Tooa 새 응용 프로그램 복원</span><span class="sxs-lookup"><span data-stu-id="2c02e-187">Restore tooa new app</span></span>
<span data-ttu-id="2c02e-188">경우에 따라는 이미 기존 응용 프로그램을 덮어쓰는 대신 백업을 복원할 때 toocreate 새 응용 프로그램을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c02e-188">Sometimes you might want toocreate a new app when you restore a backup, instead of overwriting an already existing app.</span></span> <span data-ttu-id="2c02e-189">toodo이, 변경 hello 요청 URL toopoint toohello 새 응용 프로그램, toocreate을 hello 변경 **덮어쓰기** 속성에서 JSON을 너무 hello**false**합니다.</span><span class="sxs-lookup"><span data-stu-id="2c02e-189">toodo this, change hello request URL toopoint toohello new app you want toocreate, and change hello **overwrite** property in hello JSON too**false**.</span></span>

<a name="delete-app-backup"></a>

## <a name="delete-an-app-backup"></a><span data-ttu-id="2c02e-190">앱 백업 삭제</span><span class="sxs-lookup"><span data-stu-id="2c02e-190">Delete an app backup</span></span>
<span data-ttu-id="2c02e-191">백업 toodelete, 원하는 경우 보내기는 **삭제** 요청 toohello URL **https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/ 사이트 / {name} {백업 id} /backups/**합니다.</span><span class="sxs-lookup"><span data-stu-id="2c02e-191">If you would like toodelete a backup, send a **DELETE** request toohello URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups/{backup-id}**.</span></span>

<span data-ttu-id="2c02e-192">예제 웹 사이트에 대 한 hello URL 모양을 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2c02e-192">Here is what hello URL looks like for our example website.</span></span> <span data-ttu-id="2c02e-193">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1**</span><span class="sxs-lookup"><span data-stu-id="2c02e-193">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1**</span></span>

<a name="manage-sas-url"></a>

## <a name="manage-a-backups-sas-url"></a><span data-ttu-id="2c02e-194">백업의 SAS URL 관리</span><span class="sxs-lookup"><span data-stu-id="2c02e-194">Manage a backup’s SAS URL</span></span>
<span data-ttu-id="2c02e-195">Azure 앱 서비스는 hello hello 백업을 만들 때 제공 된 SAS URL을 사용 하 여 Azure 저장소에서 백업 toodelete 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c02e-195">Azure App Service will attempt toodelete your backup from Azure Storage using hello SAS URL that was provided when hello backup was created.</span></span> <span data-ttu-id="2c02e-196">SAS URL이 올바르면 더 이상 hello 백업 hello REST API를 통해 삭제할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2c02e-196">If this SAS URL is no longer valid, hello backup cannot be deleted through hello REST API.</span></span> <span data-ttu-id="2c02e-197">그러나 hello 전송 하 여 백업과와 연결 된 SAS URL을 업데이트할 수는 **POST** 요청 toohello URL **https://management.azure.com/subscriptions/ {구독 id} /resourceGroups/ {리소스 그룹 이름} / providers/Microsoft.Web/sites/{name}/backups/{backup-id}/list**합니다.</span><span class="sxs-lookup"><span data-stu-id="2c02e-197">However, you can update hello SAS URL associated with a backup by sending a **POST** request toohello URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups/{backup-id}/list**.</span></span>

<span data-ttu-id="2c02e-198">예제 웹 사이트에 대 한 hello URL 모양을 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2c02e-198">Here is what hello URL looks like for our example website.</span></span> <span data-ttu-id="2c02e-199">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1/list**</span><span class="sxs-lookup"><span data-stu-id="2c02e-199">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1/list**</span></span>

<span data-ttu-id="2c02e-200">Hello 요청 본문에 hello 새 SAS URL이 포함 된 JSON 개체를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="2c02e-200">In hello request body, send a JSON object that contains hello new SAS URL.</span></span> <span data-ttu-id="2c02e-201">다음은 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="2c02e-201">Here is an example.</span></span>

```
{
    "properties":
    {
        "storageAccountUrl": "https://account.blob.core.windows.net/backups?sv=2015-02-21&sr=c&sig=DzlkBl7h32C8qCv%2BifdBRxE63r4iv0kZ9L7E0qP16sY%3D&se=2016-09-15T22%3A46%3A54Z&sp=rwdl"
    }
}
```

> [!NOTE]
> <span data-ttu-id="2c02e-202">보안상의 이유로 특정 백업에 대 한 GET 요청을 보낼 때 백업과와 연결 된 SAS URL hello 반환 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2c02e-202">For security reasons, hello SAS URL associated with a backup is not returned when sending a GET request for a specific backup.</span></span> <span data-ttu-id="2c02e-203">Tooview hello 백업와 연결 된 SAS URL을 사용 하도록 하려는 경우 보내기 POST 요청 toohello 위의 동일한 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="2c02e-203">If you want tooview hello SAS URL associated with a backup, send a POST request toohello same URL above.</span></span> <span data-ttu-id="2c02e-204">Hello 요청 본문에는 빈 JSON 개체를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c02e-204">Include an empty JSON object in hello request body.</span></span> <span data-ttu-id="2c02e-205">hello 응답 hello 서버에서 모든 SAS URL을 포함 하 여 해당 백업 정보를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c02e-205">hello response from hello server contains all of that backup’s information, including its SAS URL.</span></span>
> 
> 

<!-- IMAGES -->
[SampleWebsiteInformation]: ./media/websites-csm-backup/01siteconfig.png
