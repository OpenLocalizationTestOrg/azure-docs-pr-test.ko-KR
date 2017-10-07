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
# <a name="back-up-your-app-in-azure"></a>Azure에서 앱 백업
hello를 백업 및 복원 기능에 [Azure 앱 서비스](../app-service/app-service-value-prop-what-is.md) 앱 백업을 수동으로 또는 일정에 따라 쉽게 만들 수 있습니다. 덮어쓰기를 hello 기존 응용 프로그램 또는 tooanother 응용 프로그램을 복원 하 여 hello 앱 tooa 스냅숏을 이전 상태로 복원할 수 있습니다. 

앱을 백업에서 복원하는 방법에 대한 자세한 내용은 [Azure에서 앱 복원](web-sites-restore.md)을 참조하세요.

<a name="whatsbackedup"></a>

## <a name="what-gets-backed-up"></a>백업 대상
앱 서비스는 hello 다음을 백업할 수 정보 tooan Azure 저장소 계정 및 컨테이너 응용 프로그램 toouse를 구성 합니다. 

* 앱 구성
* 파일 콘텐츠
* 데이터베이스 연결 된 tooyour 응용 프로그램

hello 데이터베이스 솔루션을 다음 백업 기능으로 지원 됩니다. 
   - [SQL 데이터베이스](https://azure.microsoft.com/en-us/services/sql-database/)
   - [Azure Database for MySQL(미리 보기)](https://azure.microsoft.com/en-us/services/mysql)
   - [Azure Database for PostgreSQL(미리 보기)](https://azure.microsoft.com/en-us/services/postgres)
   - [ClearDB MySQL](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/SuccessBricksInc.ClearDBMySQLDatabase?tab=Overview)
   - [MySQL 인앱](https://blogs.msdn.microsoft.com/appserviceteam/2017/03/06/announcing-general-availability-for-mysql-in-app)
 

> [!NOTE]
>  각 백업은 증분 업데이트가 아니라 앱의 완전한 오프라인 복사본입니다.
>  

<a name="requirements"></a>

## <a name="requirements-and-restrictions"></a>요구 사항 및 제한 사항
* hello를 백업 및 복원 기능을 사용 하려면 앱 서비스 계획 toobe hello에 hello **표준** 계층 또는 **프리미엄** 계층입니다. 앱 서비스 계획 toouse 더 높은 계층 확장에 대 한 자세한 내용은 참조 [Azure에서 응용 프로그램을 수직](web-sites-scale.md)합니다.  
  **프리미엄** 계층을 사용하면 **표준** 계층보다 더 많은 매일 백업을 수행할 수 있습니다.
* Azure 저장소 계정 및 컨테이너에서 hello 필요 toobackup hello 앱과 동일한 구독 합니다. Azure 저장소 계정에 대 한 자세한 내용은 참조 hello [링크](#moreaboutstorage) hello이이 문서의 뒷부분에 있습니다.
* 응용 프로그램 및 데이터베이스 콘텐츠 too10 GB 백업 될 수 있습니다. Hello 백업 크기가이 한도 초과 하면 오류가 발생 합니다.

<a name="manualbackup"></a>

## <a name="create-a-manual-backup"></a>수동 백업 만들기
1. Hello에 [Azure 포털](https://portal.azure.com)tooyour 앱 블레이드를 탐색, 선택, **백업을**합니다. hello **백업을** 블레이드를 표시 됩니다.
   
    ![백업 페이지][ChooseBackupsPage]
   
   > [!NOTE]
   > 아래 hello 메시지를 표시 하는 경우 클릭 하기 전에 앱 서비스 계획을 진행할 수 tooupgrade 백업으로.
   > 자세한 내용은 [Azure에서 앱 확장](web-sites-scale.md) 을 참조하세요.  
   > ![저장소 계정 선택](./media/web-sites-backup/01UpgradePlan1.png)
   > 
   > 

2. Hello에 **백업** 블레이드에서 클릭 **구성**
![구성 클릭](./media/web-sites-backup/ClickConfigure1.png)
3. Hello에 **백업 구성** 블레이드에서 클릭 **저장소: 구성 되지** tooconfigure 저장소 계정입니다.
   
    ![저장소 계정 선택][ChooseStorageAccount]
4. **저장소 계정** 및 **컨테이너**를 선택하여 백업 대상을 선택합니다. hello 저장소 계정이 toohello 속해야 tooback를 원하는 hello 앱과 동일한 구독 합니다. 원하는 경우 해당 블레이드 hello에에서 새 저장소 계정 또는 새 컨테이너를 만들 수 있습니다. 완료되면 **선택**을 클릭합니다.
   
    ![저장소 계정 선택](./media/web-sites-backup/02ChooseStorageAccount1-1.png)
5. Hello에 **백업 구성** 구성할 수는 계속 열려 블레이드에서 **Backup Database**, tooinclude hello 백업 (SQL 데이터베이스 또는 MySQL)에 사용한 다음 클릭 hello 데이터베이스를 선택 합니다 **확인**합니다.  
   
    ![저장소 계정 선택](./media/web-sites-backup/03ConfigureDatabase1.png)
   
   > [!NOTE]
   > 이 목록에서 데이터베이스 tooappear에 대 한 연결 문자열 hello에 존재 해야 **연결 문자열** hello 섹션 **응용 프로그램 설정** 블레이드 앱에 대 한 합니다.
   > 
   > 
6. Hello에 **백업 구성** 블레이드에서 클릭 **저장**합니다.    
7. Hello에 **백업을** 블레이드에서 클릭 **백업**합니다.
   
    ![BackUpNow 단추][BackUpNow]
   
    Hello 백업 프로세스 중 진행 메시지를 표시 합니다.

Hello 저장소 계정 및 컨테이너 구성 되 면 언제 든 지 수동 백업을 시작할 수 있습니다.  

<a name="automatedbackups"></a>

## <a name="configure-automated-backups"></a>자동화된 백업 구성
1. Hello에 **백업 구성** 설정 블레이드에서 **예약 된 백업** 너무**에**합니다. 
   
    ![저장소 계정 선택](./media/web-sites-backup/05ScheduleBackup1.png)
2. 옵션 표시 됩니다, 백업 일정이 설정 **예약 된 백업** 너무**에**원하는 대로 hello 백업 일정을 구성 합니다. 다음을 클릭 **확인**합니다.
   
    ![자동 백업 사용][SetAutomatedBackupOn]

<a name="partialbackups"></a>

## <a name="configure-partial-backups"></a>부분 백업 구성
경우에 따라 원하지 toobackup 모든 앱에 합니다. 다음은 몇 가지 예입니다.

* 오래된 블로그 게시물이나 이미지처럼 변하지 않는 정적 콘텐츠가 포함된 앱의 [주별 백업을 설정](web-sites-backup.md#configure-automated-backups) 합니다.
* 응용 프로그램에 (즉, 한 번에 백업할 수 hello 최대 크기) 콘텐츠의 10GB 이상.
* Toobackup hello 로그 파일을 바람직하지 않습니다.

부분 백업 정확 하 게 하는 파일 수를 선택할 수 있습니다. 원하는 toobackup 합니다.

### <a name="exclude-files-from-your-backup"></a>백업에서 파일 제외
로그 파일 및 정적 이미지를 한 번 백업 되 고 toochange 진행 되지 않고 있는 앱 있다고 가정 합니다. 이러한 경우 해당 폴더와 파일을 이후의 백업에서 저장하지 않도록 제외할 수 있습니다. tooexclude 파일과 하면 백업에서 폴더 만들기는 `_backup.filter` hello에 대 한 파일 `D:\home\site\wwwroot` 응용 프로그램의 폴더입니다. 파일 및 폴더 tooexclude이이 파일에 원하는 hello 목록을 지정 합니다. 

파일은 toouse Kudu는 쉽게 tooaccess 합니다. 클릭 **고급 도구 Go->** 웹 앱 tooaccess Kudu에 대 한 설정입니다.

![포털을 사용하는 Kudu][kudu-portal]

백업에서 tooexclude 되도록 hello 폴더를 식별 합니다.  예를 들어 원하는 toofilter hello 강조 표시 된 폴더와 파일을 초과 합니다.

![Images 폴더][ImagesFolder]

파일을 만들 `_backup.filter` 위의 hello 목록 hello 파일에 저장 되지만 제거 및 `D:\home`합니다. 줄당 하나의 디렉터리 또는 파일을 나열하세요. 따라서 hello 파일의 내용을 hello 여야 합니다.
 ```bash
    \site\wwwroot\Images\brand.png
    \site\wwwroot\Images\2014
    \site\wwwroot\Images\2013
```

업로드 `_backup.filter` toohello 파일 `D:\home\site\wwwroot\` 사용 하 여 사이트의 디렉터리 [ftp](web-sites-deploy.md#ftp) 또는 다른 방법입니다. Kudu를 사용 하 여 직접 hello 파일을 만들 수 있습니다 `DebugConsole` 있습니다 hello 콘텐츠를 삽입 합니다.

동일한 실행된 백업을 hello 수행한 방식으로 일반적으로, [수동으로](#create-a-manual-backup) 또는 [자동으로](#configure-automated-backups)합니다. 이제, 파일 및 폴더에 지정 된 `_backup.filter` hello 예약 하거나 수동으로 시작 된 이후 백업에서 제외 됩니다. 

> [!NOTE]
> 사이트 hello의 부분 백업을 복원 합니다. 같은 방법으로 [일반 백업 복원](web-sites-restore.md)합니다. hello 복원 프로세스 가깝습니다를 안녕지 않습니다.
> 
> 전체 백업이 복원 되 면 hello 사이트에서 모든 콘텐츠 hello 백업에 무엇이으로 바뀝니다. 파일이 hello 사이트에 있지만 hello 백업에는 없는 경우 삭제를 가져옵니다. 하지만 부분 백업 복원 되 면 hello 차단 목록에 포함할 디렉터리 중 하나 또는 모든 블랙 리스트에 올린된 파일에 있는 모든 콘텐츠에 있는 그대로 유지 됩니다.
> 


<a name="aboutbackups"></a>

## <a name="how-backups-are-stored"></a>백업 저장 방법
Hello 백업을 hello에 표시 되는 앱에 대 한 하나 이상의 백업을 수행한 후 **컨테이너** 저장소 계정과 응용 프로그램의 블레이드에서 합니다. 각 백업 이루어져 hello 저장소 계정에는`.zip` hello 백업 데이터를 포함 하는 파일 및 `.xml` hello의 매니페스트가 포함 된 파일 `.zip` 파일 내용의 합니다. 압축을 풀 수 있으며 원하는 tooaccess 백업을 복원 하는 경우 응용 프로그램을 실제로 수행 하지 않고 경우 이러한 파일을 찾을 수 있습니다.

hello 앱에 대 한 데이터베이스 백업은 hello the.zip 파일의 hello 루트에 저장 됩니다. SQL 데이터베이스의 경우 이 파일은 BACPAC 파일(파일 확장명 없음)이며, 가져올 수 있습니다. toocreate hello BACPAC 내보내기에 따라 SQL 데이터베이스, 참조 [가져올 BACPAC 파일 tooCreate 새 사용자 데이터베이스](http://technet.microsoft.com/library/hh710052.aspx)합니다.

> [!WARNING]
> hello 파일을 변경 하면 **websitebackups** 컨테이너에 잘못 된 서명과 따라서 restorable 아닌 백업 toobecome hello 발생할 수 있습니다.
> 
> 

<a name="nextsteps"></a>

## <a name="next-steps"></a>다음 단계
앱을 백업에서 복원하는 방법에 대한 자세한 내용은 [Azure에서 앱 복원](web-sites-restore.md)을 참조하세요. 백업 하 고 REST API를 사용 하 여 앱 서비스 앱을 복원할 수도 있습니다 (참조 [사용 REST toobackup 및 복원 앱 서비스 앱](websites-csm-backup.md)).


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

