
<span data-ttu-id="a4ef9-101">Scott Hanselman과 수석 엔지니어링 관리자 Karthik Raman이 진행하는 이 Azure Friday 비디오를 통해 Azure Cosmos DB 글로벌 배포에 대해 자세히 알아 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4ef9-101">You can learn about Azure Cosmos DB global distribution in this Azure Friday video with Scott Hanselman and Principal Engineering Manager Karthik Raman.</span></span>

>[!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Planet-Scale-NoSQL-with-DocumentDB/player]  

<span data-ttu-id="a4ef9-102">글로벌 데이터베이스 복제가 Cosmos DB에서 작동하는 방법에 대한 자세한 내용은 [Cosmos DB를 사용하여 전역적으로 데이터 배포](../articles/documentdb/documentdb-distribute-data-globally.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a4ef9-102">For more information about how global database replication works in Cosmos DB, see [Distribute data globally with Cosmos DB](../articles/documentdb/documentdb-distribute-data-globally.md).</span></span>

## <span data-ttu-id="a4ef9-103"><a id="addregion"></a>Hello Azure 포털을 사용 하 여 글로벌 데이터베이스 영역 추가</span><span class="sxs-lookup"><span data-stu-id="a4ef9-103"><a id="addregion"></a>Add global database regions using hello Azure Portal</span></span>
<span data-ttu-id="a4ef9-104">Azure Cosmos DB는 전세계 모든 [Azure 지역][azureregions]에 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="a4ef9-104">Azure Cosmos DB is available in all [Azure regions][azureregions] world-wide.</span></span> <span data-ttu-id="a4ef9-105">데이터베이스 계정에 대 한 기본 일관성 수준이 hello를 선택한 후 (선택 사항에 따라 기본 일관성 수준 및 글로벌 배포 요구) 하나 이상의 영역을 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4ef9-105">After selecting hello default consistency level for your database account, you can associate one or more regions (depending on your choice of default consistency level and global distribution needs).</span></span>

1. <span data-ttu-id="a4ef9-106">Hello에 [Azure 포털](https://portal.azure.com/)hello 왼쪽된 막대에서 클릭 **Azure Cosmos DB**합니다.</span><span class="sxs-lookup"><span data-stu-id="a4ef9-106">In hello [Azure portal](https://portal.azure.com/), in hello left bar, click **Azure Cosmos DB**.</span></span>
2. <span data-ttu-id="a4ef9-107">Hello에 **Azure Cosmos DB** 블레이드, 선택 hello 데이터베이스 계정 toomodify 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4ef9-107">In hello **Azure Cosmos DB** blade, select hello database account toomodify.</span></span>
3. <span data-ttu-id="a4ef9-108">Hello 계정 블레이드에서 클릭 **데이터를 전역적으로 복제** hello 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4ef9-108">In hello account blade, click **Replicate data globally** from hello menu.</span></span>
4. <span data-ttu-id="a4ef9-109">Hello에 **데이터를 전역적으로 복제** 블레이드에서 hello 영역 tooadd 또는 hello 맵에서 영역을 클릭 하 여 제거할 선택한 다음 클릭 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="a4ef9-109">In hello **Replicate data globally** blade, select hello regions tooadd or remove by clicking regions in hello map, and then click **Save**.</span></span> <span data-ttu-id="a4ef9-110">비용 tooadding 영역은 hello를 참조 하십시오 [가격 책정 페이지](https://azure.microsoft.com/pricing/details/documentdb/) 또는 hello [DocumentDB 전역적으로 사용 데이터를 분산](../articles/documentdb/documentdb-distribute-data-globally.md) 대 한 자세한 내용은 문서.</span><span class="sxs-lookup"><span data-stu-id="a4ef9-110">There is a cost tooadding regions, see hello [pricing page](https://azure.microsoft.com/pricing/details/documentdb/) or hello [Distribute data globally with DocumentDB](../articles/documentdb/documentdb-distribute-data-globally.md) article for more information.</span></span>
   
    ![Hello 맵 tooadd의 hello 영역을 클릭 하거나 해당 구성 요소 제거][1]
    
<span data-ttu-id="a4ef9-112">두 번째 영역을 추가한 후 hello **수동 장애 조치** hello에서 옵션이 설정 되어 **데이터를 전역적으로 복제** 블레이드 hello 포털에서입니다.</span><span class="sxs-lookup"><span data-stu-id="a4ef9-112">Once you add a second region, hello **Manual Failover** option is enabled on hello **Replicate data globally** blade in hello portal.</span></span> <span data-ttu-id="a4ef9-113">이 옵션 tootest hello 장애 조치 프로세스를 사용 하거나 hello 주 쓰기 지역을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4ef9-113">You can use this option tootest hello failover process or change hello primary write region.</span></span> <span data-ttu-id="a4ef9-114">세 번째 영역을 추가한 후 hello **장애 조치 우선 순위** 에서 옵션이 설정 되어 읽기에 대 한 hello 장애 조치 순서를 변경할 수 있도록 동일한 블레이드 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4ef9-114">Once you add a third region, hello **Failover Priorities** option is enabled on hello same blade so that you can change hello failover order for reads.</span></span>  

### <a name="selecting-global-database-regions"></a><span data-ttu-id="a4ef9-115">글로벌 데이터베이스 지역 선택</span><span class="sxs-lookup"><span data-stu-id="a4ef9-115">Selecting global database regions</span></span>
<span data-ttu-id="a4ef9-116">둘 이상의 지역을 구성하기 위한 두 가지 일반적인 시나리오는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a4ef9-116">There are two common scenarios for configuring two or more regions:</span></span>

1. <span data-ttu-id="a4ef9-117">Hello 전 세계 있는 위치에 관계 없이 toodata tooend 사용자 대기 시간이 짧은 액세스를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4ef9-117">Delivering low-latency access toodata tooend users no matter where they are located around hello globe</span></span>
2. <span data-ttu-id="a4ef9-118">BCDR(무중단 업무 방식 및 재해 복구)를 위한 지역 복원 기능 추가</span><span class="sxs-lookup"><span data-stu-id="a4ef9-118">Adding regional resiliency for business continuity and disaster recovery (BCDR)</span></span>

<span data-ttu-id="a4ef9-119">전달 하기 위한 대기 시간이 짧은 tooend-사용자에 대 한 응용 프로그램 hello 및 toowhere hello 응용 프로그램의 사용자는 해당 하는 hello 지역에서 Azure Cosmos DB가 있는 추가 모두 toodeploy를 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="a4ef9-119">For delivering low-latency tooend-users, it is recommended toodeploy both hello application and add Azure Cosmos DB in hello regions thats correspond toowhere hello application's users are located.</span></span>

<span data-ttu-id="a4ef9-120">BCDR, 것이 좋습니다 hello에 설명 된 hello 지역 쌍에 따라 tooadd 영역의 [비즈니스 연속성 및 재해 복구 (BCDR): Azure 쌍을 이루는 지역] [ bcdr] 문서.</span><span class="sxs-lookup"><span data-stu-id="a4ef9-120">For BCDR, it is recommended tooadd regions based on hello region pairs described in hello [Business continuity and disaster recovery (BCDR): Azure Paired Regions][bcdr] article.</span></span>

<!--

## <a id="selectwriteregion"></a>Select hello write region

While all regions associated with your Cosmos DB database account can serve reads (both, single item as well as multi-item paginated reads) and queries, only one region can actively receive hello write (insert, upsert, replace, delete) requests. tooset hello active write region, do hello following  


1. In hello **Azure Cosmos DB** blade, select hello database account toomodify.
2. In hello account blade, click **Replicate data globally** from hello menu.
3. In hello **Replicate data globally** blade, click **Manual Failover** from hello top bar.
    ![Change hello write region under Azure Cosmos DB Account > Replicate data globally > Manual Failover][2]
4. Select a read region toobecome hello new write region, click hello checkbox tooconfirm triggering a failover, and click OK
    ![Change hello write region by selecting a new region in list under Azure Cosmos DB Account > Replicate data globally > Manual Failover][3]

--->

<!--Image references-->
[1]: ./media/cosmos-db-tutorial-global-distribution-portal/azure-cosmos-db-add-region.png
[2]: ./media/cosmos-db-tutorial-global-distribution-portal/azure-cosmos-db-manual-failover-1.png
[3]: ./media/cosmos-db-tutorial-global-distribution-portal/azure-cosmos-db-manual-failover-2.png

<!--Reference style links - using these makes hello source content way more readable than using inline links-->
[bcdr]: https://azure.microsoft.com/documentation/articles/best-practices-availability-paired-regions/
[consistency]: ../articles/cosmos-db/consistency-levels.md
[azureregions]: https://azure.microsoft.com/regions/#services
[offers]: https://azure.microsoft.com/pricing/details/cosmos-db/
