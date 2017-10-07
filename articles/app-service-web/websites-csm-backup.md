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
# <a name="use-rest-tooback-up-and-restore-app-service-apps"></a>앱 서비스 앱을 복원 및 REST tooback 사용 하 여
> [!div class="op_single_selector"]
> * [PowerShell](../app-service/app-service-powershell-backup.md)
> * [REST API](websites-csm-backup.md)
> 
> 

[Azure 서비스 앱](https://azure.microsoft.com/services/app-service/web/) 을 Azure 저장소에 blob로 백업할 수 있습니다. hello 백업 hello 응용 프로그램의 데이터베이스를 포함할 수도 있습니다. Hello 앱도 실수로 삭제 된, 또는 hello 앱 요구 toobe tooa 이전 버전 되돌려 진 경우에 모든 이전 백업에서 복원할 수 있습니다. 필요할 때 언제든지 백업할 수 있으며, 적당한 간격으로 백업을 예약할 수도 있습니다.

이 문서에서는 toobackup 및 복원 RESTful API를 사용 하 여 앱 요청 하는 방식에 대해 설명 합니다. Toocreate 같은 hello Azure 포털을 통해 그래픽으로 응용 프로그램 백업 관리는 경우 참조 [Azure 앱 서비스의 웹 앱 백업](web-sites-backup.md)

<a name="gettingstarted"></a>

## <a name="getting-started"></a>시작하기
toosend REST 요청, 응용 프로그램의 tooknow 필요한 **이름**, **리소스 그룹**, 및 **구독 id**합니다. Hello에서 응용 프로그램을 클릭 하 여이 정보를 찾을 수 **앱 서비스** hello의 블레이드에서 [Azure 포털](https://portal.azure.com)합니다. 이 문서의 예제 hello에 대 한 구성 하는 hello 웹 사이트 **backuprestoreapiexamples.azurewebsites.net**합니다. Hello WestUS-Web-기본 리소스 그룹에 저장 하 고 hello ID 00001111-2222-3333-4444-555566667777 인 구독에서 실행 되 고 합니다.

![샘플 웹 사이트 정보][SampleWebsiteInformation]

<a name="backup-restore-rest-api"></a>

## <a name="backup-and-restore-rest-api"></a>REST API 백업 및 복원
이제 여러 가지 예 toouse REST API toobackup hello 하 고 응용 프로그램을 복원 하는 방법을 설명 합니다. 각 예제에는 URL 및 HTTP 요청 본문이 포함되어 있습니다. hello 샘플 URL {구독 id} 등의 중괄호에 래핑된 자리 표시자를 포함 합니다. 앱에 대 한 해당 정보를 hello hello 자리 표시자를 바꿉니다. 참조용으로 hello Url 예에에서 표시 되는 각 자리 표시자에 대 한 설명을 다음과 같습니다.

* 구독 id-hello Azure 구독 포함 hello 응용 프로그램의 ID
* 리소스 그룹 이름-hello 리소스 그룹 포함 hello 앱의 이름
* 이름-hello 응용 프로그램의 이름
* 백업-id-ID hello 응용 프로그램 백업

Hello hello API의 전체 설명서를 hello 참조 hello HTTP 요청에 포함 될 수 있는 여러 가지 선택적 매개 변수를 포함 하 여 [Azure 리소스 탐색기](https://resources.azure.com/)합니다.

<a name="backup-on-demand"></a>

## <a name="backup-an-app-on-demand"></a>주문형 앱 백업
응용 프로그램을 tooback 즉시 보냅니다는 **POST** 너무 요청**https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/ 백업 /**합니다.

다음은 예제 웹 사이트를 사용 하 여 모양 hello URL입니다. **https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backup/**

저장소 계정 toouse toostore hello 백업 하 여 요청 toospecify의 hello 본문에서 JSON 개체를 제공 합니다. hello JSON 개체 라는 속성이 있어야 합니다. **storageAccountUrl**를 보유 하는 [SAS URL](../storage/common/storage-dotnet-shared-access-signature-part-1.md) 쓰기 액세스 toohello Azure 저장소 컨테이너 hello 백업 blob을 포함 하는 권한을 부여 합니다. 데이터베이스를 tooback 하려는 경우 hello 이름, 유형 및 백업 hello 데이터베이스 toobe의 연결 문자열을 포함 하는 목록도 제공 해야 합니다.

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

Hello 응용 프로그램의 백업을 즉시 hello 요청을 받으면 시작 됩니다. hello 백업 프로세스는 시간이 오래 toocomplete를 걸릴 수 있습니다. HTTP 응답 hello 다른 요청 toosee hello hello 백업 상태에서 사용할 수 있는 ID를 포함 합니다. Hello hello HTTP 응답 tooour 백업 요청 본문의 예를 들면 다음과 같습니다.

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
> 오류 메시지의 HTTP 응답 hello hello log 속성에서 찾을 수 있습니다.
> 
> 

<a name="schedule-automatic-backups"></a>

## <a name="schedule-automatic-backups"></a>자동 백업 예약
필요에 따라 앱을 추가 toobacking, 백업 toohappen을 예약할 자동으로 수 있습니다.

### <a name="set-up-a-new-automatic-backup-schedule"></a>새로운 자동 백업 일정 설정
백업 일정을 tooset 보내기는 **배치** 너무 요청**https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/config 백업/**합니다.

예제 웹 사이트에 대 한 hello URL 모양을 다음과 같습니다. **https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/config/backup**

hello 요청 본문에는 hello 백업 구성을 지정 하는 JSON 개체가 있어야 합니다. 모든 필요한 hello 매개 변수가 있는 예를 들면 다음과 같습니다.

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

이 예제에서는 구성 hello 앱 toobe 7 일 마다 자동으로 백업 합니다. 매개 변수를 hello **frequencyInterval** 및 **frequencyUnit** 얼마나 자주 hello 백업을 수행할를 결정 합니다. **frequencyUnit**에 유효한 값은 **시간** 및 **일**입니다. 예를 들어, 12 시간 마다 앱을 tooback frequencyInterval too12 및 frequencyUnit toohour를 설정 합니다.

오래 된 백업 hello 저장소 계정에서 자동으로 제거 됩니다. 오래 된 hello hello 설정 하 여 백업 수를 제어할 수 있습니다 **retentionPeriodInDays** 매개 변수입니다. Tooalways 백업이 하나 이상 설정 되어, 오래 된 정도 관계 없이 저장 하려면 **keepAtLeastOneBackup** tootrue 합니다.

### <a name="get-hello-automatic-backup-schedule"></a>Hello 자동 백업 일정 가져오기
tooget 응용 프로그램의 백업 구성, 전송 된 **POST** 요청 toohello URL **https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/ 사이트 / {name} / config/백업/목록**합니다.

이 예제에서는 사이트에 대 한 hello URL은 **https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/config/backup/list**합니다.

<a name="get-backup-status"></a>

## <a name="get-hello-status-of-a-backup"></a>백업 hello 상태를 가져옵니다.
Hello 앱 크기에 따라 이면 백업에는 시간이 걸릴 수 toocomplete 합니다. 또한 백업이 실패하거나, 시간이 초과되거나, 부분적으로 성공할 수 있습니다. 모든 응용 프로그램의 백업의 toosee hello 상태 보내기는 **가져오기** 요청 toohello URL **https://management.azure.com/subscriptions/ {구독 id} {리소스 그룹 이름} /resourceGroups/ /providers/ Microsoft.Web/sites/{name}/backups**합니다.

특정 백업 toosee hello 상태 GET 요청 toohello URL 보내기 **https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups/ { 백업-id}**합니다.

예제 웹 사이트에 대 한 hello URL 모양을 다음과 같습니다. **https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1**

hello 응답 본문에는 JSON 개체 유사한 toothis 예 포함 되어 있습니다.

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

hello 한 백업 상태는 열거 형식입니다. 다음과 같은 상태가 가능합니다.

* 0 – InProgress: hello 백업 시작 되었지만 아직 완료 되지 않았습니다.
* 1 – 실패: hello 백업 하지 못했습니다.
* 2 – 성공된: hello 백업이 성공적으로 완료 되었습니다.
* 3 – TimedOut: hello 백업 시간에 마치지 못함 및 취소 되었습니다.
* 4 –: hello 백업 요청 큐에 대기 만들어지지만 시작 되지 않았습니다.
* 5 – 생략: hello 백업을 계속할 수 없습니다 인해 너무 많은 백업을 트리거하지 tooa 일정.
* 6-PartiallySucceeded: hello 백업 성공 했지만 일부 파일이 백업 되지 않은 이러한를 읽을 수 없습니다. 이 문제는 일반적으로 배타적 잠금이 hello 파일에 배치 하기 때문에 발생 합니다.
* 7-DeleteInProgress: hello 백업을 삭제 하는 요청 된 toobe 되었지만 아직 삭제 되지 않은 합니다.
* 8-삭제 실패: hello 백업을 삭제할 수 없습니다. 이 SAS URL을 사용 하는 toocreate hello 백업 hello 만료 되었기 때문에 발생할 수 있습니다.
* 9-삭제 됨: hello 백업 삭제 했습니다.

<a name="restore-app"></a>

## <a name="restore-an-app-from-a-backup"></a>백업으로 앱 복원
응용 프로그램 삭제 되었거나 또는 toorevert 응용 프로그램 tooa 이전 버전을 사용할 경우 백업에서 hello 응용 프로그램을 복원할 수 있습니다. tooinvoke 복원 하는 보내기는 **POST** 요청 toohello URL **https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/ 백업 / {백업 id} / 복원**합니다.

예제 웹 사이트에 대 한 hello URL 모양을 다음과 같습니다. **https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1/restore**

Hello 요청 본문에 hello 복원 작업에 대 한 hello 속성을 포함 하는 JSON 개체를 보냅니다. 다음은 필요한 속성이 모두 포함된 예제입니다.

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

### <a name="restore-tooa-new-app"></a>Tooa 새 응용 프로그램 복원
경우에 따라는 이미 기존 응용 프로그램을 덮어쓰는 대신 백업을 복원할 때 toocreate 새 응용 프로그램을 할 수 있습니다. toodo이, 변경 hello 요청 URL toopoint toohello 새 응용 프로그램, toocreate을 hello 변경 **덮어쓰기** 속성에서 JSON을 너무 hello**false**합니다.

<a name="delete-app-backup"></a>

## <a name="delete-an-app-backup"></a>앱 백업 삭제
백업 toodelete, 원하는 경우 보내기는 **삭제** 요청 toohello URL **https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/ 사이트 / {name} {백업 id} /backups/**합니다.

예제 웹 사이트에 대 한 hello URL 모양을 다음과 같습니다. **https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1**

<a name="manage-sas-url"></a>

## <a name="manage-a-backups-sas-url"></a>백업의 SAS URL 관리
Azure 앱 서비스는 hello hello 백업을 만들 때 제공 된 SAS URL을 사용 하 여 Azure 저장소에서 백업 toodelete 시도 합니다. SAS URL이 올바르면 더 이상 hello 백업 hello REST API를 통해 삭제할 수 없습니다. 그러나 hello 전송 하 여 백업과와 연결 된 SAS URL을 업데이트할 수는 **POST** 요청 toohello URL **https://management.azure.com/subscriptions/ {구독 id} /resourceGroups/ {리소스 그룹 이름} / providers/Microsoft.Web/sites/{name}/backups/{backup-id}/list**합니다.

예제 웹 사이트에 대 한 hello URL 모양을 다음과 같습니다. **https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1/list**

Hello 요청 본문에 hello 새 SAS URL이 포함 된 JSON 개체를 보냅니다. 다음은 예제입니다.

```
{
    "properties":
    {
        "storageAccountUrl": "https://account.blob.core.windows.net/backups?sv=2015-02-21&sr=c&sig=DzlkBl7h32C8qCv%2BifdBRxE63r4iv0kZ9L7E0qP16sY%3D&se=2016-09-15T22%3A46%3A54Z&sp=rwdl"
    }
}
```

> [!NOTE]
> 보안상의 이유로 특정 백업에 대 한 GET 요청을 보낼 때 백업과와 연결 된 SAS URL hello 반환 되지 않습니다. Tooview hello 백업와 연결 된 SAS URL을 사용 하도록 하려는 경우 보내기 POST 요청 toohello 위의 동일한 URL입니다. Hello 요청 본문에는 빈 JSON 개체를 포함 합니다. hello 응답 hello 서버에서 모든 SAS URL을 포함 하 여 해당 백업 정보를 포함 합니다.
> 
> 

<!-- IMAGES -->
[SampleWebsiteInformation]: ./media/websites-csm-backup/01siteconfig.png
