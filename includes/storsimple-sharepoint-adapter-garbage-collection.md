<!--author=SharS last changed: 9/17/15-->

<span data-ttu-id="70fd4-101">이 절차에서는 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="70fd4-101">In this procedure, you will:</span></span>

1. <span data-ttu-id="70fd4-102">[Toorun hello 유지 관리자 실행 파일을 준비](#to-prepare-to-run-the-maintainer) 합니다.</span><span class="sxs-lookup"><span data-stu-id="70fd4-102">[Prepare toorun hello Maintainer executable](#to-prepare-to-run-the-maintainer) .</span></span>
2. <span data-ttu-id="70fd4-103">[분리 된 Blob의 즉시 삭제에 대 한 hello 콘텐츠 데이터베이스 및 휴지통 준비](#to-prepare-the-content-database-and-recycle-bin-to-immediately-delete-orphaned-blobs)합니다.</span><span class="sxs-lookup"><span data-stu-id="70fd4-103">[Prepare hello content database and Recycle Bin for immediate deletion of orphaned BLOBs](#to-prepare-the-content-database-and-recycle-bin-to-immediately-delete-orphaned-blobs).</span></span>
3. <span data-ttu-id="70fd4-104">[Maintainer.exe를 실행합니다](#to-run-the-maintainer).</span><span class="sxs-lookup"><span data-stu-id="70fd4-104">[Run Maintainer.exe](#to-run-the-maintainer).</span></span>
4. <span data-ttu-id="70fd4-105">[Hello 콘텐츠 데이터베이스 및 휴지통을 활성화 설정이 되돌릴](#to-revert-the-content-database-and-recycle-bin-settings)합니다.</span><span class="sxs-lookup"><span data-stu-id="70fd4-105">[Revert hello content database and Recycle Bin settings](#to-revert-the-content-database-and-recycle-bin-settings).</span></span>

#### <a name="tooprepare-toorun-hello-maintainer"></a><span data-ttu-id="70fd4-106">tooprepare toorun hello 유지 관리자</span><span class="sxs-lookup"><span data-stu-id="70fd4-106">tooprepare toorun hello Maintainer</span></span>
1. <span data-ttu-id="70fd4-107">Hello 웹 프런트 엔드 서버에서 관리자 권한으로 SharePoint 2013 관리 셸 hello를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="70fd4-107">On hello Web front-end server, open hello SharePoint 2013 Management Shell as an administrator.</span></span>
2. <span data-ttu-id="70fd4-108">Toohello 폴더 탐색 *드라이브 부팅*: files\microsoft SQL Remote Blob Storage 10.50\Maintainer\.</span><span class="sxs-lookup"><span data-stu-id="70fd4-108">Navigate toohello folder *boot drive*:\Program Files\Microsoft SQL Remote Blob Storage 10.50\Maintainer\.</span></span>
3. <span data-ttu-id="70fd4-109">이름 바꾸기 **Microsoft.Data.SqlRemoteBlobs.Maintainer.exe.config** 너무**web.config**합니다.</span><span class="sxs-lookup"><span data-stu-id="70fd4-109">Rename **Microsoft.Data.SqlRemoteBlobs.Maintainer.exe.config** too**web.config**.</span></span>
4. <span data-ttu-id="70fd4-110">사용 하 여 `aspnet_regiis -pdf connectionStrings` toodecrypt hello web.config 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="70fd4-110">Use `aspnet_regiis -pdf connectionStrings` toodecrypt hello web.config file.</span></span>
5. <span data-ttu-id="70fd4-111">Hello에서 hello 암호 해독 된 web.config 파일에서 `connectionStrings` 노드를 SQL server 인스턴스에 대 한 연결 문자열 hello를 추가 하 고 hello 콘텐츠 데이터베이스 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="70fd4-111">In hello decrypted web.config file, under hello `connectionStrings` node, add hello connection string for your SQL server instance and hello content database name.</span></span> <span data-ttu-id="70fd4-112">다음 예제는 hello를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="70fd4-112">See hello following example.</span></span>
   
    `<add name=”RBSMaintainerConnectionWSSContent” connectionString="Data Source=SHRPT13-SQL12\SHRPT13;Initial Catalog=WSS_Content;Integrated Security=True;Application Name=&quot;Remote Blob Storage Maintainer for WSS_Content&quot;" providerName="System.Data.SqlClient" />`
6. <span data-ttu-id="70fd4-113">사용 하 여 `aspnet_regiis –pef connectionStrings` toore-hello web.config 파일을 암호화 합니다.</span><span class="sxs-lookup"><span data-stu-id="70fd4-113">Use `aspnet_regiis –pef connectionStrings` toore-encrypt hello web.config file.</span></span> 
7. <span data-ttu-id="70fd4-114">Web.config tooMicrosoft.Data.SqlRemoteBlobs.Maintainer.exe.config을 이름을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="70fd4-114">Rename web.config tooMicrosoft.Data.SqlRemoteBlobs.Maintainer.exe.config.</span></span> 

#### <a name="tooprepare-hello-content-database-and-recycle-bin-tooimmediately-delete-orphaned-blobs"></a><span data-ttu-id="70fd4-115">tooprepare hello 콘텐츠 데이터베이스 및 휴지통 tooimmediately 분리 된 Blob을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="70fd4-115">tooprepare hello content database and Recycle Bin tooimmediately delete orphaned BLOBs</span></span>
1. <span data-ttu-id="70fd4-116">Hello SQL Management Studio에서 SQL Server에서 hello 다음 hello 대상 콘텐츠 데이터베이스에 대 한 업데이트 쿼리를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="70fd4-116">On hello SQL Server, in SQL Management Studio, run hello following update queries for hello target content database:</span></span> 
   
       `use WSS_Content`
   
       `exec mssqlrbs.rbs_sp_set_config_value ‘garbage_collection_time_window’ , ’time 00:00:00’`
   
       `exec mssqlrbs.rbs_sp_set_config_value ‘delete_scan_period’ , ’time 00:00:00’`
2. <span data-ttu-id="70fd4-117">Hello에 웹 프런트 엔드 서버, 아래에서 **중앙 관리**, hello 편집 **웹 응용 프로그램의 일반 설정** hello 원하는 콘텐츠 데이터베이스 tootemporarily 사용 안 함 hello 휴지통에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="70fd4-117">On hello web front-end server, under **Central Administration**, edit hello **Web Application General Settings** for hello desired content database tootemporarily disable hello Recycle Bin.</span></span> <span data-ttu-id="70fd4-118">이 작업은 모든 관련된 사이트 모음에 대해 빈 hello 휴지통을 활성화 합니다.</span><span class="sxs-lookup"><span data-stu-id="70fd4-118">This action will also empty hello Recycle Bin for any related site collections.</span></span> <span data-ttu-id="70fd4-119">toodo이를 클릭 하이 여 **중앙 관리** -> **응용 프로그램 관리** -> **웹 응용 프로그램 (웹 응용 프로그램 관리)**  ->  **SharePoint-80** -> **일반 응용 프로그램 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="70fd4-119">toodo this, click **Central Administration** -> **Application Management** -> **Web Applications (Manage web applications)** -> **SharePoint - 80** -> **General Application Settings**.</span></span> <span data-ttu-id="70fd4-120">집합 hello **휴지통 상태** 너무**OFF**합니다.</span><span class="sxs-lookup"><span data-stu-id="70fd4-120">Set hello **Recycle Bin Status** too**OFF**.</span></span>
   
    ![웹 응용 프로그램의 일반 설정](./media/storsimple-sharepoint-adapter-garbage-collection/HCS_WebApplicationGeneralSettings-include.png)

#### <a name="toorun-hello-maintainer"></a><span data-ttu-id="70fd4-122">toorun hello 유지 관리자</span><span class="sxs-lookup"><span data-stu-id="70fd4-122">toorun hello Maintainer</span></span>
* <span data-ttu-id="70fd4-123">Hello 웹 프런트 엔드 서버에서 SharePoint 2013 관리 셸 hello에 hello 유지 관리자 다음과 같이 실행:</span><span class="sxs-lookup"><span data-stu-id="70fd4-123">On hello web front-end server, in hello SharePoint 2013 Management Shell, run hello Maintainer as follows:</span></span>
  
      `Microsoft.Data.SqlRemoteBlobs.Maintainer.exe -ConnectionStringName RBSMaintainerConnectionWSSContent -Operation GarbageCollection -GarbageCollectionPhases rdo`
  
  > [!NOTE]
  > <span data-ttu-id="70fd4-124">Hello만 `GarbageCollection` 이 이번에 StorSimple에 대 한 작업은 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="70fd4-124">Only hello `GarbageCollection` operation is supported for StorSimple at this time.</span></span> <span data-ttu-id="70fd4-125">또한 참고가 Microsoft.Data.SqlRemoteBlobs.Maintainer.exe에 대해 실행 하는 hello 매개 변수는 대/소문자 구분.</span><span class="sxs-lookup"><span data-stu-id="70fd4-125">Also note that hello parameters issued for Microsoft.Data.SqlRemoteBlobs.Maintainer.exe are case sensitive.</span></span> 
  > 
  > 

#### <a name="toorevert-hello-content-database-and-recycle-bin-settings"></a><span data-ttu-id="70fd4-126">toorevert hello 콘텐츠 데이터베이스 및 휴지통 설정</span><span class="sxs-lookup"><span data-stu-id="70fd4-126">toorevert hello content database and Recycle Bin settings</span></span>
1. <span data-ttu-id="70fd4-127">Hello SQL Management Studio에서 SQL Server에서 hello 다음 hello 대상 콘텐츠 데이터베이스에 대 한 업데이트 쿼리를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="70fd4-127">On hello SQL Server, in SQL Management Studio, run hello following update queries for hello target content database:</span></span>
   
      `use WSS_Content`
   
      `exec mssqlrbs.rbs_sp_set_config_value ‘garbage_collection_time_window’ , ‘days 30’`
   
      `exec mssqlrbs.rbs_sp_set_config_value ‘delete_scan_period’ , ’days 30’`
   
      `exec mssqlrbs.rbs_sp_set_config_value ‘orphan_scan_period’ , ’days 30’`
2. <span data-ttu-id="70fd4-128">Hello 웹 프런트 엔드 서버에서의 **중앙 관리**, hello 편집 **웹 응용 프로그램의 일반 설정** hello 원하는 콘텐츠 데이터베이스 toore enable hello 휴지통에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="70fd4-128">On hello web front-end server, in **Central Administration**, edit hello **Web Application General Settings** for hello desired content database toore-enable hello Recycle Bin.</span></span> <span data-ttu-id="70fd4-129">toodo이를 클릭 하이 여 **중앙 관리** -> **응용 프로그램 관리** -> **웹 응용 프로그램 (웹 응용 프로그램 관리)**  ->  **SharePoint-80** -> **일반 응용 프로그램 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="70fd4-129">toodo this, click **Central Administration** -> **Application Management** -> **Web Applications (Manage web applications)** -> **SharePoint - 80** -> **General Application Settings**.</span></span> <span data-ttu-id="70fd4-130">너무 hello 휴지통 상태 설정**ON**합니다.</span><span class="sxs-lookup"><span data-stu-id="70fd4-130">Set hello Recycle Bin Status too**ON**.</span></span>

