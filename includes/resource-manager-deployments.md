## <a name="incremental-and-complete-deployments"></a><span data-ttu-id="9b17c-101">증분 및 전체 배포</span><span class="sxs-lookup"><span data-stu-id="9b17c-101">Incremental and complete deployments</span></span>
<span data-ttu-id="9b17c-102">리소스를 배포할 때는 hello 배포는 증분 업데이트 또는 완전 한 업데이트를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b17c-102">When deploying your resources, you specify that hello deployment is either an incremental update or a complete update.</span></span> <span data-ttu-id="9b17c-103">이러한 두 모드 간에 hello 주요 차이점은 리소스 관리자가 hello 서식 파일에 없는 hello 리소스 그룹에 기존 리소스를 처리 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="9b17c-103">hello primary difference between these two modes is how Resource Manager handles existing resources in hello resource group that are not in hello template:</span></span>

* <span data-ttu-id="9b17c-104">완료 모드에서는 리소스 관리자 **삭제** hello 리소스 그룹에 존재 하지만 hello 서식 파일에 지정 되지 않은 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="9b17c-104">In complete mode, Resource Manager **deletes** resources that exist in hello resource group but are not specified in hello template.</span></span> 
* <span data-ttu-id="9b17c-105">증분 모드에서 리소스 관리자 **변경 하지 않습니다** hello 리소스 그룹에 존재 하지만 hello 서식 파일에 지정 되지 않은 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="9b17c-105">In incremental mode, Resource Manager **leaves unchanged** resources that exist in hello resource group but are not specified in hello template.</span></span>

<span data-ttu-id="9b17c-106">두 모드에 대 한 리소스 관리자 hello 서식 파일에 지정 된 모든 리소스 tooprovision을 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b17c-106">For both modes, Resource Manager attempts tooprovision all resources specified in hello template.</span></span> <span data-ttu-id="9b17c-107">Hello 리소스가 hello 리소스 그룹에 이미 존재 하는 경우 해당 설정을 변경 하지 않습니다 hello 작업으로 인해 변경 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9b17c-107">If hello resource already exists in hello resource group and its settings are unchanged, hello operation results in no change.</span></span> <span data-ttu-id="9b17c-108">리소스에 대 한 hello 설정을 변경 하면 이러한 새 설정을 사용 하 여 hello 리소스 프로 비전 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9b17c-108">If you change hello settings for a resource, hello resource is provisioned with those new settings.</span></span> <span data-ttu-id="9b17c-109">Tooupdate hello의 위치나 유형에 기존 리소스를 시도 하면 오류가 발생 하 여 hello 배포가 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b17c-109">If you attempt tooupdate hello location or type of an existing resource, hello deployment fails with an error.</span></span> <span data-ttu-id="9b17c-110">대신, hello 위치를 사용 하 여 새 리소스를 배포 하거나 해야 하는 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b17c-110">Instead, deploy a new resource with hello location or type that you need.</span></span>

<span data-ttu-id="9b17c-111">기본적으로 리소스 관리자는 증분 모드 hello를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9b17c-111">By default, Resource Manager uses hello incremental mode.</span></span>

<span data-ttu-id="9b17c-112">증분 및 전체 모드 간의 tooillustrate hello 차이 hello를 시나리오를 따르는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="9b17c-112">tooillustrate hello difference between incremental and complete modes, consider hello following scenario.</span></span>

<span data-ttu-id="9b17c-113">**기존 리소스 그룹**은 다음 항목을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="9b17c-113">**Existing Resource Group** contains:</span></span>

* <span data-ttu-id="9b17c-114">리소스 A</span><span class="sxs-lookup"><span data-stu-id="9b17c-114">Resource A</span></span>
* <span data-ttu-id="9b17c-115">리소스 B</span><span class="sxs-lookup"><span data-stu-id="9b17c-115">Resource B</span></span>
* <span data-ttu-id="9b17c-116">리소스 C</span><span class="sxs-lookup"><span data-stu-id="9b17c-116">Resource C</span></span>

<span data-ttu-id="9b17c-117">**템플릿**은 다음 항목을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="9b17c-117">**Template** defines:</span></span>

* <span data-ttu-id="9b17c-118">리소스 A</span><span class="sxs-lookup"><span data-stu-id="9b17c-118">Resource A</span></span>
* <span data-ttu-id="9b17c-119">리소스 B</span><span class="sxs-lookup"><span data-stu-id="9b17c-119">Resource B</span></span>
* <span data-ttu-id="9b17c-120">리소스 D</span><span class="sxs-lookup"><span data-stu-id="9b17c-120">Resource D</span></span>

<span data-ttu-id="9b17c-121">에 배포 되어 **증분** 모드 hello 리소스 그룹 포함:</span><span class="sxs-lookup"><span data-stu-id="9b17c-121">When deployed in **incremental** mode, hello resource group contains:</span></span>

* <span data-ttu-id="9b17c-122">리소스 A</span><span class="sxs-lookup"><span data-stu-id="9b17c-122">Resource A</span></span>
* <span data-ttu-id="9b17c-123">리소스 B</span><span class="sxs-lookup"><span data-stu-id="9b17c-123">Resource B</span></span>
* <span data-ttu-id="9b17c-124">리소스 C</span><span class="sxs-lookup"><span data-stu-id="9b17c-124">Resource C</span></span>
* <span data-ttu-id="9b17c-125">리소스 D</span><span class="sxs-lookup"><span data-stu-id="9b17c-125">Resource D</span></span>

<span data-ttu-id="9b17c-126">리소스 C가 **전체** 모드로 배포된 경우 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="9b17c-126">When deployed in **complete** mode, Resource C is deleted.</span></span> <span data-ttu-id="9b17c-127">hello 리소스 그룹에 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b17c-127">hello resource group contains:</span></span>

* <span data-ttu-id="9b17c-128">리소스 A</span><span class="sxs-lookup"><span data-stu-id="9b17c-128">Resource A</span></span>
* <span data-ttu-id="9b17c-129">리소스 B</span><span class="sxs-lookup"><span data-stu-id="9b17c-129">Resource B</span></span>
* <span data-ttu-id="9b17c-130">리소스 D</span><span class="sxs-lookup"><span data-stu-id="9b17c-130">Resource D</span></span>
