<!--author=SharS last changed: 9/17/15-->

<span data-ttu-id="2c5ee-101">이 절차에서는 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="2c5ee-101">In this procedure, you will:</span></span>

1. <span data-ttu-id="2c5ee-102">[유지 관리자 실행 파일을 실행할 준비를 합니다](#to-prepare-to-run-the-maintainer) .</span><span class="sxs-lookup"><span data-stu-id="2c5ee-102">[Prepare to run the Maintainer executable](#to-prepare-to-run-the-maintainer) .</span></span>
2. <span data-ttu-id="2c5ee-103">[분리된 BLOB의 즉시 삭제를 위해 콘텐츠 데이터베이스 및 휴지통을 준비합니다](#to-prepare-the-content-database-and-recycle-bin-to-immediately-delete-orphaned-blobs).</span><span class="sxs-lookup"><span data-stu-id="2c5ee-103">[Prepare the content database and Recycle Bin for immediate deletion of orphaned BLOBs](#to-prepare-the-content-database-and-recycle-bin-to-immediately-delete-orphaned-blobs).</span></span>
3. <span data-ttu-id="2c5ee-104">[Maintainer.exe를 실행합니다](#to-run-the-maintainer).</span><span class="sxs-lookup"><span data-stu-id="2c5ee-104">[Run Maintainer.exe](#to-run-the-maintainer).</span></span>
4. <span data-ttu-id="2c5ee-105">[콘텐츠 데이터베이스 및 휴지통 설정을 되돌립니다](#to-revert-the-content-database-and-recycle-bin-settings).</span><span class="sxs-lookup"><span data-stu-id="2c5ee-105">[Revert the content database and Recycle Bin settings](#to-revert-the-content-database-and-recycle-bin-settings).</span></span>

#### <a name="to-prepare-to-run-the-maintainer"></a><span data-ttu-id="2c5ee-106">유지 관리자 실행을 준비하려면</span><span class="sxs-lookup"><span data-stu-id="2c5ee-106">To prepare to run the Maintainer</span></span>
1. <span data-ttu-id="2c5ee-107">웹 프런트 엔드 서버에서 SharePoint 2013 관리 셸을 관리자 권한으로 엽니다.</span><span class="sxs-lookup"><span data-stu-id="2c5ee-107">On the Web front-end server, open the SharePoint 2013 Management Shell as an administrator.</span></span>
2. <span data-ttu-id="2c5ee-108">*부팅 드라이브*:\Program Files\Microsoft SQL Remote Blob Storage 10.50\Maintainer\. 폴더로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="2c5ee-108">Navigate to the folder *boot drive*:\Program Files\Microsoft SQL Remote Blob Storage 10.50\Maintainer\.</span></span>
3. <span data-ttu-id="2c5ee-109">**Microsoft.Data.SqlRemoteBlobs.Maintainer.exe.config**의 이름을 **web.config**로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="2c5ee-109">Rename **Microsoft.Data.SqlRemoteBlobs.Maintainer.exe.config** to **web.config**.</span></span>
4. <span data-ttu-id="2c5ee-110">`aspnet_regiis -pdf connectionStrings` 를 사용하여 web.config 파일의 암호를 해독합니다.</span><span class="sxs-lookup"><span data-stu-id="2c5ee-110">Use `aspnet_regiis -pdf connectionStrings` to decrypt the web.config file.</span></span>
5. <span data-ttu-id="2c5ee-111">암호 해독된 web.config 파일의 `connectionStrings` 노드에 SQL Server 인스턴스 및 콘텐츠 데이터베이스 이름에 대한 연결 문자열을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2c5ee-111">In the decrypted web.config file, under the `connectionStrings` node, add the connection string for your SQL server instance and the content database name.</span></span> <span data-ttu-id="2c5ee-112">다음 예제를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2c5ee-112">See the following example.</span></span>
   
    `<add name=”RBSMaintainerConnectionWSSContent” connectionString="Data Source=SHRPT13-SQL12\SHRPT13;Initial Catalog=WSS_Content;Integrated Security=True;Application Name=&quot;Remote Blob Storage Maintainer for WSS_Content&quot;" providerName="System.Data.SqlClient" />`
6. <span data-ttu-id="2c5ee-113">`aspnet_regiis –pef connectionStrings` 를 사용하여 web.config 파일을 다시 암호화합니다.</span><span class="sxs-lookup"><span data-stu-id="2c5ee-113">Use `aspnet_regiis –pef connectionStrings` to re-encrypt the web.config file.</span></span> 
7. <span data-ttu-id="2c5ee-114">web.config의 이름을 Microsoft.Data.SqlRemoteBlobs.Maintainer.exe.config로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="2c5ee-114">Rename web.config to Microsoft.Data.SqlRemoteBlobs.Maintainer.exe.config.</span></span> 

#### <a name="to-prepare-the-content-database-and-recycle-bin-to-immediately-delete-orphaned-blobs"></a><span data-ttu-id="2c5ee-115">분리된 BLOB을 즉시 삭제하기 위한 콘텐츠 데이터베이스 및 휴지통을 준비하려면</span><span class="sxs-lookup"><span data-stu-id="2c5ee-115">To prepare the content database and Recycle Bin to immediately delete orphaned BLOBs</span></span>
1. <span data-ttu-id="2c5ee-116">SQL Server의 SQL Management Studio에서 대상 콘텐츠 데이터베이스에 대한 다음 업데이트 쿼리를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="2c5ee-116">On the SQL Server, in SQL Management Studio, run the following update queries for the target content database:</span></span> 
   
       `use WSS_Content`
   
       `exec mssqlrbs.rbs_sp_set_config_value ‘garbage_collection_time_window’ , ’time 00:00:00’`
   
       `exec mssqlrbs.rbs_sp_set_config_value ‘delete_scan_period’ , ’time 00:00:00’`
2. <span data-ttu-id="2c5ee-117">웹 프런트 엔드 서버의 **중앙 관리**에서 원하는 콘텐츠 데이터베이스에 대한 **웹 응용 프로그램의 일반 설정**을 편집하여 휴지통을 일시적으로 사용하지 않도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="2c5ee-117">On the web front-end server, under **Central Administration**, edit the **Web Application General Settings** for the desired content database to temporarily disable the Recycle Bin.</span></span> <span data-ttu-id="2c5ee-118">또한 이 작업은 관련 사이트 모음에 대한 휴지통을 비웁니다.</span><span class="sxs-lookup"><span data-stu-id="2c5ee-118">This action will also empty the Recycle Bin for any related site collections.</span></span> <span data-ttu-id="2c5ee-119">이 작업을 수행하려면 **중앙 관리** -> **응용 프로그램 관리** -> **웹 응용 프로그램(웹 응용 프로그램 관리)** -> **SharePoint - 80** -> **일반 응용 프로그램 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2c5ee-119">To do this, click **Central Administration** -> **Application Management** -> **Web Applications (Manage web applications)** -> **SharePoint - 80** -> **General Application Settings**.</span></span> <span data-ttu-id="2c5ee-120">**휴지통 상태**를 **OFF**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="2c5ee-120">Set the **Recycle Bin Status** to **OFF**.</span></span>
   
    ![웹 응용 프로그램의 일반 설정](./media/storsimple-sharepoint-adapter-garbage-collection/HCS_WebApplicationGeneralSettings-include.png)

#### <a name="to-run-the-maintainer"></a><span data-ttu-id="2c5ee-122">유지 관리자를 실행하려면</span><span class="sxs-lookup"><span data-stu-id="2c5ee-122">To run the Maintainer</span></span>
* <span data-ttu-id="2c5ee-123">다음과 같이 웹 프런트 엔드 서버의 SharePoint 2013 관리 셸에서 유지 관리자를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="2c5ee-123">On the web front-end server, in the SharePoint 2013 Management Shell, run the Maintainer as follows:</span></span>
  
      `Microsoft.Data.SqlRemoteBlobs.Maintainer.exe -ConnectionStringName RBSMaintainerConnectionWSSContent -Operation GarbageCollection -GarbageCollectionPhases rdo`
  
  > [!NOTE]
  > <span data-ttu-id="2c5ee-124">지금은 StorSimple에 대해 `GarbageCollection` 작업만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="2c5ee-124">Only the `GarbageCollection` operation is supported for StorSimple at this time.</span></span> <span data-ttu-id="2c5ee-125">Microsoft.Data.SqlRemoteBlobs.Maintainer.exe에 대한 실행 매개 변수는 대/소문자를 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="2c5ee-125">Also note that the parameters issued for Microsoft.Data.SqlRemoteBlobs.Maintainer.exe are case sensitive.</span></span> 
  > 
  > 

#### <a name="to-revert-the-content-database-and-recycle-bin-settings"></a><span data-ttu-id="2c5ee-126">콘텐츠 데이터베이스 및 휴지통 설정을 되돌리려면</span><span class="sxs-lookup"><span data-stu-id="2c5ee-126">To revert the content database and Recycle Bin settings</span></span>
1. <span data-ttu-id="2c5ee-127">SQL Server의 SQL Management Studio에서 대상 콘텐츠 데이터베이스에 대한 다음 업데이트 쿼리를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="2c5ee-127">On the SQL Server, in SQL Management Studio, run the following update queries for the target content database:</span></span>
   
      `use WSS_Content`
   
      `exec mssqlrbs.rbs_sp_set_config_value ‘garbage_collection_time_window’ , ‘days 30’`
   
      `exec mssqlrbs.rbs_sp_set_config_value ‘delete_scan_period’ , ’days 30’`
   
      `exec mssqlrbs.rbs_sp_set_config_value ‘orphan_scan_period’ , ’days 30’`
2. <span data-ttu-id="2c5ee-128">웹 프런트 엔드 서버의 **중앙 관리**에서 원하는 콘텐츠 데이터베이스에 대한 **웹 응용 프로그램의 일반 설정**을 편집하여 휴지통을 다시 사용할 수 있도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="2c5ee-128">On the web front-end server, in **Central Administration**, edit the **Web Application General Settings** for the desired content database to re-enable the Recycle Bin.</span></span> <span data-ttu-id="2c5ee-129">이 작업을 수행하려면 **중앙 관리** -> **응용 프로그램 관리** -> **웹 응용 프로그램(웹 응용 프로그램 관리)** -> **SharePoint - 80** -> **일반 응용 프로그램 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2c5ee-129">To do this, click **Central Administration** -> **Application Management** -> **Web Applications (Manage web applications)** -> **SharePoint - 80** -> **General Application Settings**.</span></span> <span data-ttu-id="2c5ee-130">휴지통 상태를 **ON**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="2c5ee-130">Set the Recycle Bin Status to **ON**.</span></span>

