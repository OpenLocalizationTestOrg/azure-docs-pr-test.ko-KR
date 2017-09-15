
<!--
includes/sql-data-warehouse-include-pause-description.md

Latest Freshness check:  2016-04-22 , barbkess.

As of circa 2016-04-22, the following topics might include this include:
articles/sql-data-warehouse/sql-data-warehouse-manage-scale-out-tasks.md
articles/sql-data-warehouse/sql-data-warehouse-manage-scale-out-tasks-powershell.md
articles/sql-data-warehouse/sql-data-warehouse-manage-scale-out-tasks-rest-api.md

-->
<span data-ttu-id="adb3d-101">비용을 절약하기 위해 필요에 따라 계산 리소스를 일지 중지 및 다시 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="adb3d-101">To save costs, you can pause and resume compute resources on-demand.</span></span> <span data-ttu-id="adb3d-102">예를 들어, 밤 시간과 주말에 데이터베이스를 사용하지 않으려면 해당 시간에 일시 중지했다가 주간에 다시 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="adb3d-102">For example, if you won't be using the database during the night and on weekends, you can pause it during those times, and resume it during the day.</span></span> <span data-ttu-id="adb3d-103">데이터베이스 일시 중지 중에는 DWU 요금이 부과되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="adb3d-103">You won't be charged for DWUs while the database is paused.</span></span>

<span data-ttu-id="adb3d-104">데이터베이스를 일시 중지하면</span><span class="sxs-lookup"><span data-stu-id="adb3d-104">When you pause a database:</span></span>

* <span data-ttu-id="adb3d-105">계산 및 메모리 리소스가 데이터 센터에서 사용 가능한 리소스의 풀에 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="adb3d-105">Compute and memory resources are returned to the pool of available resources in the data center</span></span>
* <span data-ttu-id="adb3d-106">일시 중지 중에는 DWU 비용이 0입니다.</span><span class="sxs-lookup"><span data-stu-id="adb3d-106">DWU costs are zero for the duration of the pause.</span></span>
* <span data-ttu-id="adb3d-107">데이터 저장소에는 영향이 없으며 데이터는 그대로 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="adb3d-107">Data storage is not affected and your data stays intact.</span></span> 
* <span data-ttu-id="adb3d-108">SQL 데이터 웨어하우스가 실행 중이거나 큐에 있는 모든 작업을 취소합니다.</span><span class="sxs-lookup"><span data-stu-id="adb3d-108">SQL Data Warehouse cancels all running or queued operations.</span></span>

