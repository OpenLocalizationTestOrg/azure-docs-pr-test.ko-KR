<!--author=SharS last changed: 1/14/2016 -->

> [!NOTE]
> <span data-ttu-id="b8c50-101">SharePoint RBS 구성에 대 한 변경 내용을 toohello StorSimple 어댑터를 만들 때 toohello Domain Admins 그룹에 속하는 사용자 계정으로 로그온 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8c50-101">When making changes toohello StorSimple Adapter for SharePoint RBS configuration, you must be logged on with a user account that belongs toohello Domain Admins group.</span></span> <span data-ttu-id="b8c50-102">또한 hello 구성 페이지 hello 중앙 관리 같은 호스트에서 실행 되는 브라우저에서 액세스 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8c50-102">Additionally, you must access hello configuration page from a browser running on hello same host as Central Administration.</span></span>
> 
> 

#### <a name="tooconfigure-rbs"></a><span data-ttu-id="b8c50-103">RBS tooconfigure</span><span class="sxs-lookup"><span data-stu-id="b8c50-103">tooconfigure RBS</span></span>
1. <span data-ttu-id="b8c50-104">Hello SharePoint 중앙 관리 페이지를 열고 너무 찾아보기**시스템 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="b8c50-104">Open hello SharePoint Central Administration page, and browse too**System Settings**.</span></span> 
2. <span data-ttu-id="b8c50-105">Hello에 **Azure StorSimple** 섹션에서 클릭 **StorSimple 어댑터 구성**합니다.</span><span class="sxs-lookup"><span data-stu-id="b8c50-105">In hello **Azure StorSimple** section, click **Configure StorSimple Adapter**.</span></span>
   
    ![Hello StorSimple 어댑터 구성](./media/storsimple-sharepoint-adapter-configure-rbs/HCS_SSASP_ConfigRBS1-include.png) 
3. <span data-ttu-id="b8c50-107">Hello에 **StorSimple 어댑터 구성** 페이지:</span><span class="sxs-lookup"><span data-stu-id="b8c50-107">On hello **Configure StorSimple Adapter** page:</span></span>
   
   1. <span data-ttu-id="b8c50-108">해당 hello 있는지 확인 **경로 편집 사용** 확인란을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8c50-108">Make sure that hello **Enable editing path** check box is selected.</span></span>
   2. <span data-ttu-id="b8c50-109">Hello 텍스트 상자에 hello BLOB 저장소의 hello 범용 명명 규칙 (UNC) 경로 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8c50-109">In hello text box, type hello Universal Naming Convention (UNC) path of hello BLOB store.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="b8c50-110">hello BLOB 저장소 볼륨 hello StorSimple 장치에 구성 된 iSCSI 볼륨에서 호스팅해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8c50-110">hello BLOB store volume must be hosted on an iSCSI volume configured on hello StorSimple device.</span></span>

   3. <span data-ttu-id="b8c50-111">Hello 클릭 **사용** 각 원격 저장소에 대 한 tooconfigure 되도록 hello 콘텐츠 데이터베이스 아래 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="b8c50-111">Click hello **Enable** button below each of hello content databases that you want tooconfigure for remote storage.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="b8c50-112">hello BLOB 저장소에 공유 하 고 연결할 모든 웹 프런트 엔드 (WFE) 서버에 의해 여야 합니다. 및 hello SharePoint 서버 팜에 대해 구성 된 hello 사용자 계정 액세스 toohello 공유에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8c50-112">hello BLOB store must be shared and reachable by all web front-end (WFE) servers, and hello user account that is configured for hello SharePoint server farm must have access toohello share.</span></span>
      
      ![Hello RBS 공급자를 사용 하도록 설정](./media/storsimple-sharepoint-adapter-configure-rbs/HCS_SSASP_ConfigRBS2-include.png)
      
      <span data-ttu-id="b8c50-114">RBS를 사용 하지 않도록 설정 하거나 설정할 때 hello 메시지의 뒤에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="b8c50-114">When you enable or disable RBS, you will also see hello following message.</span></span>
      
      ![StorSimple 어댑터 사용 또는 사용 안함 구성](./media/storsimple-sharepoint-adapter-configure-rbs/HCS_ConfigureStorSimpleAdapterEnableDisableMessage-include.png)

   4. <span data-ttu-id="b8c50-116">Hello 클릭 **업데이트** 단추 tooapply hello 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8c50-116">Click hello **Update** button tooapply hello configuration.</span></span> <span data-ttu-id="b8c50-117">Hello를 클릭할 때 **업데이트** 단추를 hello RBS 구성 상태가 모든 WFE 서버에서 업데이트 되 고 hello 전체 팜에서 RBS 사용 하도록 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8c50-117">When you click hello **Update** button, hello RBS configuration status will be updated on all WFE servers, and hello entire farm will be RBS-enabled.</span></span> <span data-ttu-id="b8c50-118">hello 메시지의 뒤에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="b8c50-118">hello following message appears.</span></span>
      
      ![어댑터 구성 메시지](./media/storsimple-sharepoint-adapter-configure-rbs/HCS_SSASP_ConfigRBS3-include.png)
      
      > [!NOTE]
      > <span data-ttu-id="b8c50-120">매우 많은 (200 보다 큼) 데이터베이스와 SharePoint 팜에 대해 RBS를 구성 하는 경우 hello SharePoint 중앙 관리 웹 페이지 시간이 초과 될 수 있습니다. 이 경우 hello 페이지를 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="b8c50-120">If you are configuring RBS for a SharePoint farm with a very large number of databases (greater than 200), hello SharePoint Central Administration web page might time out. If that occurs, refresh hello page.</span></span> <span data-ttu-id="b8c50-121">Hello 구성 프로세스에는 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b8c50-121">This does not affect hello configuration process.</span></span>

4. <span data-ttu-id="b8c50-122">Hello 구성을 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="b8c50-122">Verify hello configuration:</span></span>
   
   1. <span data-ttu-id="b8c50-123">Toohello SharePoint 중앙 관리 웹 사이트에 로그인 하 고 toohello 찾아보기 **StorSimple 어댑터 구성** 페이지.</span><span class="sxs-lookup"><span data-stu-id="b8c50-123">Log on toohello SharePoint Central Administration website, and browse toohello **Configure StorSimple Adapter** page.</span></span>
   2. <span data-ttu-id="b8c50-124">Hello 구성 세부 정보 toomake hello 설정을 입력 한 일치 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8c50-124">Check hello configuration details toomake sure that they match hello settings that you entered.</span></span> 
5. <span data-ttu-id="b8c50-125">RBS가 올바르게 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b8c50-125">Verify that RBS works correctly:</span></span>
   
   1. <span data-ttu-id="b8c50-126">문서 tooSharePoint 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8c50-126">Upload a document tooSharePoint.</span></span> 
   2. <span data-ttu-id="b8c50-127">사용자가 구성한 toohello UNC 경로를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="b8c50-127">Browse toohello UNC path that you configured.</span></span> <span data-ttu-id="b8c50-128">Hello RBS 디렉터리 구조를 만든 다음 업로드 hello 개체 포함 하 고 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8c50-128">Make sure that hello RBS directory structure was created and that it contains hello uploaded object.</span></span>
6. <span data-ttu-id="b8c50-129">(선택 사항) Hello Microsoft RBS를 사용할 수 있습니다 `Migrate()` SharePoint toomigrate 기존 BLOB 콘텐츠 toohello StorSimple 장치에 포함 된 PowerShell cmdlet.</span><span class="sxs-lookup"><span data-stu-id="b8c50-129">(Optional) You can use hello Microsoft RBS `Migrate()` PowerShell cmdlet included with SharePoint toomigrate existing BLOB content toohello StorSimple device.</span></span> <span data-ttu-id="b8c50-130">자세한 내용은 참조 [로 또는 SharePoint 2013에서 RBS에서 콘텐츠를 마이그레이션하고] [ 6] 또는 [로 또는 RBS (SharePoint Foundation 2010)에서 콘텐츠를 마이그레이션하고] [7].</span><span class="sxs-lookup"><span data-stu-id="b8c50-130">For more information, see [Migrate content into or out of RBS in SharePoint 2013][6] or [Migrate content into or out of RBS (SharePoint Foundation 2010)][7].</span></span>
7. <span data-ttu-id="b8c50-131">(선택 사항) 테스트 설치 시 hello Blob 다음과 같이 hello 콘텐츠 데이터베이스 외부로 이동 된 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8c50-131">(Optional) On test installations, you can verify that hello BLOBs were moved out of hello content database as follows:</span></span> 
   
   1. <span data-ttu-id="b8c50-132">SQL Management Studio를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b8c50-132">Start SQL Management Studio.</span></span>
   2. <span data-ttu-id="b8c50-133">다음과 같이 hello ListBlobsInDB_2010.sql 또는 ListBlobsInDB_2013.sql 쿼리를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8c50-133">Run hello ListBlobsInDB_2010.sql or ListBlobsInDB_2013.sql query, as follows.</span></span>
      
      ```
      **ListBlobsInDB_2013.sql**
      
        USE WSS_Content
        GO
      
        SELECT DocStreams.DocId,
      
               LeafName AS Name,
               Content,
               AllDocs.Size AS OrigSizeOfContent,
               LEN(CAST(Content AS VARBINARY(MAX))) AS SizeOfContentInDB,
               DocStreams.RbsId,
               TimeLastModified
      
        FROM DocStreams
      
             INNER JOIN AllDocs ON DocStreams.DocId = AllDocs.Id
        ORDER BY TimeLastModified DESC
        GO
      
      **ListBlobsInDB_2010.sql**
      
        USE WSS_Content
        GO
      
        SELECT AllDocStreams.Id,
      
               LeafName AS Name,
               Content,
               AllDocs.Size AS OrigSizeOfContent,
               LEN(CAST(Content AS VARBINARY(MAX))) AS SizeOfContentInDB,
               RbsId,
               TimeLastModified
        FROM AllDocStreams
      
             INNER JOIN AllDocs ON AllDocStreams.Id = AllDocs.Id
        ORDER BY TimeLastModified DESC
        GO
      ```
      
      <span data-ttu-id="b8c50-134">RBS가 올바르게 구성 업로드 되어 RBS로 성공적으로 표면화 된 모든 개체에 대 한 hello SizeOfContentInDB 열에 NULL 값이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8c50-134">If RBS was configured correctly, a NULL value should appear in hello SizeOfContentInDB column for any object that was uploaded and successfully externalized with RBS.</span></span>
8. <span data-ttu-id="b8c50-135">(선택 사항) RBS를 구성 하 고 모든 BLOB 콘텐츠 toohello StorSimple 장치로 이동 hello 콘텐츠 데이터베이스 toohello 장치 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8c50-135">(Optional) After you configure RBS and move all BLOB content toohello StorSimple device, you can move hello content database toohello device.</span></span> <span data-ttu-id="b8c50-136">Toomove hello 콘텐츠 데이터베이스를 선택 하면 기본 볼륨으로 hello 장치에서 hello 콘텐츠 데이터베이스 저장소를 구성 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b8c50-136">If you choose toomove hello content database, we recommend that you configure hello content database storage on hello device as a primary volume.</span></span> <span data-ttu-id="b8c50-137">그런 다음 사용 하 여 SQL Server 모범 사례 toomigrate hello 콘텐츠 데이터베이스 toohello StorSimple 장치를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8c50-137">Then, use established SQL Server best practices toomigrate hello content database toohello StorSimple device.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="b8c50-138">Hello StorSimple 8000 시리즈 (것은 지원 되지 않습니다 hello 5000 또는 7000 시리즈에 대 한)에 대 한 이동 hello 콘텐츠 데이터베이스 toohello 장치 에서만 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8c50-138">Moving hello content database toohello device is only supported for hello StorSimple 8000 series (it is not supported for hello 5000 or 7000 series).</span></span>
   
   <span data-ttu-id="b8c50-139">Blob 및 콘텐츠 데이터베이스 hello hello StorSimple 장치의 별도 볼륨에 저장 하면 hello에 구성 하는 것이 좋습니다 같은 볼륨 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="b8c50-139">If you store BLOBs and hello content database in separate volumes on hello StorSimple device, we recommend that you configure them in hello same volume container.</span></span> <span data-ttu-id="b8c50-140">이렇게 하면 같이 백업됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8c50-140">This ensures that they will be backed up together.</span></span>
   
   > [!WARNING]
   > <span data-ttu-id="b8c50-141">RBS를 설정 하지 않은 경우 hello 콘텐츠 데이터베이스 toohello StorSimple 장치를 이동 하지 않는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b8c50-141">If you have not enabled RBS, we do not recommend moving hello content database toohello StorSimple device.</span></span> <span data-ttu-id="b8c50-142">테스트되지 않은 구성입니다.</span><span class="sxs-lookup"><span data-stu-id="b8c50-142">This is an untested configuration.</span></span>
   
9. <span data-ttu-id="b8c50-143">다음 단계로 이동 toohello: [가비지 수집 구성](#configure-garbage-collection)합니다.</span><span class="sxs-lookup"><span data-stu-id="b8c50-143">Go toohello next step: [Configure garbage collection](#configure-garbage-collection).</span></span>

[6]: https://technet.microsoft.com/library/ff628254(v=office.15).aspx
[7]: https://technet.microsoft.com/library/ff628255(v=office.14).aspx
