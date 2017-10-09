<!--author=SharS last changed: 9/17/15-->

이 절차에서는 다음을 수행합니다.

1. [Toorun hello 유지 관리자 실행 파일을 준비](#to-prepare-to-run-the-maintainer) 합니다.
2. [분리 된 Blob의 즉시 삭제에 대 한 hello 콘텐츠 데이터베이스 및 휴지통 준비](#to-prepare-the-content-database-and-recycle-bin-to-immediately-delete-orphaned-blobs)합니다.
3. [Maintainer.exe를 실행합니다](#to-run-the-maintainer).
4. [Hello 콘텐츠 데이터베이스 및 휴지통을 활성화 설정이 되돌릴](#to-revert-the-content-database-and-recycle-bin-settings)합니다.

#### <a name="tooprepare-toorun-hello-maintainer"></a>tooprepare toorun hello 유지 관리자
1. Hello 웹 프런트 엔드 서버에서 관리자 권한으로 SharePoint 2013 관리 셸 hello를 엽니다.
2. Toohello 폴더 탐색 *드라이브 부팅*: files\microsoft SQL Remote Blob Storage 10.50\Maintainer\.
3. 이름 바꾸기 **Microsoft.Data.SqlRemoteBlobs.Maintainer.exe.config** 너무**web.config**합니다.
4. 사용 하 여 `aspnet_regiis -pdf connectionStrings` toodecrypt hello web.config 파일입니다.
5. Hello에서 hello 암호 해독 된 web.config 파일에서 `connectionStrings` 노드를 SQL server 인스턴스에 대 한 연결 문자열 hello를 추가 하 고 hello 콘텐츠 데이터베이스 이름입니다. 다음 예제는 hello를 참조 하십시오.
   
    `<add name=”RBSMaintainerConnectionWSSContent” connectionString="Data Source=SHRPT13-SQL12\SHRPT13;Initial Catalog=WSS_Content;Integrated Security=True;Application Name=&quot;Remote Blob Storage Maintainer for WSS_Content&quot;" providerName="System.Data.SqlClient" />`
6. 사용 하 여 `aspnet_regiis –pef connectionStrings` toore-hello web.config 파일을 암호화 합니다. 
7. Web.config tooMicrosoft.Data.SqlRemoteBlobs.Maintainer.exe.config을 이름을 바꿉니다. 

#### <a name="tooprepare-hello-content-database-and-recycle-bin-tooimmediately-delete-orphaned-blobs"></a>tooprepare hello 콘텐츠 데이터베이스 및 휴지통 tooimmediately 분리 된 Blob을 삭제합니다.
1. Hello SQL Management Studio에서 SQL Server에서 hello 다음 hello 대상 콘텐츠 데이터베이스에 대 한 업데이트 쿼리를 실행 합니다. 
   
       `use WSS_Content`
   
       `exec mssqlrbs.rbs_sp_set_config_value ‘garbage_collection_time_window’ , ’time 00:00:00’`
   
       `exec mssqlrbs.rbs_sp_set_config_value ‘delete_scan_period’ , ’time 00:00:00’`
2. Hello에 웹 프런트 엔드 서버, 아래에서 **중앙 관리**, hello 편집 **웹 응용 프로그램의 일반 설정** hello 원하는 콘텐츠 데이터베이스 tootemporarily 사용 안 함 hello 휴지통에 대 한 합니다. 이 작업은 모든 관련된 사이트 모음에 대해 빈 hello 휴지통을 활성화 합니다. toodo이를 클릭 하이 여 **중앙 관리** -> **응용 프로그램 관리** -> **웹 응용 프로그램 (웹 응용 프로그램 관리)**  ->  **SharePoint-80** -> **일반 응용 프로그램 설정**합니다. 집합 hello **휴지통 상태** 너무**OFF**합니다.
   
    ![웹 응용 프로그램의 일반 설정](./media/storsimple-sharepoint-adapter-garbage-collection/HCS_WebApplicationGeneralSettings-include.png)

#### <a name="toorun-hello-maintainer"></a>toorun hello 유지 관리자
* Hello 웹 프런트 엔드 서버에서 SharePoint 2013 관리 셸 hello에 hello 유지 관리자 다음과 같이 실행:
  
      `Microsoft.Data.SqlRemoteBlobs.Maintainer.exe -ConnectionStringName RBSMaintainerConnectionWSSContent -Operation GarbageCollection -GarbageCollectionPhases rdo`
  
  > [!NOTE]
  > Hello만 `GarbageCollection` 이 이번에 StorSimple에 대 한 작업은 지원 합니다. 또한 참고가 Microsoft.Data.SqlRemoteBlobs.Maintainer.exe에 대해 실행 하는 hello 매개 변수는 대/소문자 구분. 
  > 
  > 

#### <a name="toorevert-hello-content-database-and-recycle-bin-settings"></a>toorevert hello 콘텐츠 데이터베이스 및 휴지통 설정
1. Hello SQL Management Studio에서 SQL Server에서 hello 다음 hello 대상 콘텐츠 데이터베이스에 대 한 업데이트 쿼리를 실행 합니다.
   
      `use WSS_Content`
   
      `exec mssqlrbs.rbs_sp_set_config_value ‘garbage_collection_time_window’ , ‘days 30’`
   
      `exec mssqlrbs.rbs_sp_set_config_value ‘delete_scan_period’ , ’days 30’`
   
      `exec mssqlrbs.rbs_sp_set_config_value ‘orphan_scan_period’ , ’days 30’`
2. Hello 웹 프런트 엔드 서버에서의 **중앙 관리**, hello 편집 **웹 응용 프로그램의 일반 설정** hello 원하는 콘텐츠 데이터베이스 toore enable hello 휴지통에 대 한 합니다. toodo이를 클릭 하이 여 **중앙 관리** -> **응용 프로그램 관리** -> **웹 응용 프로그램 (웹 응용 프로그램 관리)**  ->  **SharePoint-80** -> **일반 응용 프로그램 설정**합니다. 너무 hello 휴지통 상태 설정**ON**합니다.

