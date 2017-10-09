
<span data-ttu-id="853a3-101">Microsoft Azure 클라우드 서비스의 문제 진단 필요 hello 문제가 발생 하는 대로 가상 컴퓨터에서 hello 서비스의 로그 파일을 수집 합니다.</span><span class="sxs-lookup"><span data-stu-id="853a3-101">Diagnosing issues with an Microsoft Azure cloud service requires collecting hello service’s log files on virtual machines as hello issues occur.</span></span> <span data-ttu-id="853a3-102">요청 시 AzureLogCollector 확장 hello tooperfom 일회성 원격으로 로그온 하지 않고도 – 하나 이상의 클라우드 서비스 Vm (웹 역할 및 작업자 역할) 및 전송 수집 hello 파일 tooan Azure 저장소 계정에서 로그 수집을 사용할 수 있습니다. hello Vm의 tooany 합니다.</span><span class="sxs-lookup"><span data-stu-id="853a3-102">You can use hello AzureLogCollector extension on-demand tooperfom one-time collection of logs from one or more Cloud Service VMs (from both web roles and worker roles) and transfer hello collected files tooan Azure storage account – all without remotely logging on tooany of hello VMs.</span></span>

> [!NOTE]
> <span data-ttu-id="853a3-103">대부분의 hello 기록 정보에 대 한 설명은 http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.asp에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="853a3-103">Descriptions for most of hello logged information can be found at http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.asp.</span></span>
> 
> 

<span data-ttu-id="853a3-104">Hello 유형의 파일 toobe 수집에 종속는 컬렉션의 두 가지 모드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="853a3-104">There are two modes of collection dependent on hello types of files toobe collected.</span></span>

* <span data-ttu-id="853a3-105">Azure 게스트 에이전트만 로그(GA).</span><span class="sxs-lookup"><span data-stu-id="853a3-105">Azure Guest Agent Logs only (GA).</span></span> <span data-ttu-id="853a3-106">이 컬렉션 모드는 모든 hello 로그 관련된 tooAzure 게스트 에이전트 및 기타 Azure 구성 요소를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="853a3-106">This collection mode includes all hello logs related tooAzure guest agents and other Azure components.</span></span>
* <span data-ttu-id="853a3-107">모든 로그(전체).</span><span class="sxs-lookup"><span data-stu-id="853a3-107">All Logs (Full).</span></span> <span data-ttu-id="853a3-108">이 컬렉션 모드는 GA 모드에서 모든 파일을 수집합니다. 또한 다음을 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="853a3-108">This collection mode will collect all files in GA mode plus:</span></span>
  
  * <span data-ttu-id="853a3-109">시스템 및 응용 프로그램 이벤트 로그</span><span class="sxs-lookup"><span data-stu-id="853a3-109">system and application event logs</span></span>
  * <span data-ttu-id="853a3-110">HTTP 오류 로그</span><span class="sxs-lookup"><span data-stu-id="853a3-110">HTTP error logs</span></span>
  * <span data-ttu-id="853a3-111">IIS 로그</span><span class="sxs-lookup"><span data-stu-id="853a3-111">IIS Logs</span></span>
  * <span data-ttu-id="853a3-112">설정 로그</span><span class="sxs-lookup"><span data-stu-id="853a3-112">Setup logs</span></span>
  * <span data-ttu-id="853a3-113">기타 시스템 로그</span><span class="sxs-lookup"><span data-stu-id="853a3-113">other system logs</span></span>

<span data-ttu-id="853a3-114">두 컬렉션 모드에서 추가 데이터 수집 폴더 구조를 다음 hello의 컬렉션을 사용 하 여 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="853a3-114">In both collection modes, additional data collection folders can be specified by using a collection of hello following structure:</span></span>

* <span data-ttu-id="853a3-115">**이름**: 수집 hello 이름 hello hello zip 파일 toobe 내의 하위 폴더 이름으로 사용 되는 hello 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="853a3-115">**Name**: hello name of hello collection, which will be used as hello name of subfolder inside hello zip file toobe collected.</span></span>
* <span data-ttu-id="853a3-116">**위치**: hello 경로 toohello 폴더에 hello 가상 컴퓨터 파일에 수집 됩니다.</span><span class="sxs-lookup"><span data-stu-id="853a3-116">**Location**: hello path toohello folder on hello virtual machine where file will be collected.</span></span>
* <span data-ttu-id="853a3-117">**SearchPattern**: hello 패턴의 파일 toobe hello 이름 수집 합니다.</span><span class="sxs-lookup"><span data-stu-id="853a3-117">**SearchPattern**: hello pattern of hello names of files toobe collected.</span></span> <span data-ttu-id="853a3-118">기본값은 “*”입니다.</span><span class="sxs-lookup"><span data-stu-id="853a3-118">Default is “*”</span></span>
* <span data-ttu-id="853a3-119">**재귀**: 경우 hello 파일 hello 폴더 아래에 재귀적으로 수집할지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="853a3-119">**Recursive**: if hello files will be collected recursively under hello folder.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="853a3-120">필수 조건</span><span class="sxs-lookup"><span data-stu-id="853a3-120">Prerequisites</span></span>
* <span data-ttu-id="853a3-121">확장 toosave 생성 된 zip 파일에 대 한 저장소 계정을 toohave를 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="853a3-121">You need toohave a storage account for extension toosave generated zip files.</span></span>
* <span data-ttu-id="853a3-122">Azure PowerShell Cmdlets V0.8.0 이상을 사용하고 있는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="853a3-122">You must make sure that you are using Azure PowerShell Cmdlets V0.8.0 or above.</span></span> <span data-ttu-id="853a3-123">자세한 내용은 [Azure 다운로드](https://azure.microsoft.com/downloads/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="853a3-123">For more information, see [Azure Downloads](https://azure.microsoft.com/downloads/).</span></span>

## <a name="add-hello-extension"></a><span data-ttu-id="853a3-124">Hello 확장 추가</span><span class="sxs-lookup"><span data-stu-id="853a3-124">Add hello extension</span></span>
<span data-ttu-id="853a3-125">사용할 수 있습니다 [Microsoft Azure PowerShell](https://msdn.microsoft.com/library/dn495240.aspx) cmdlet 또는 [서비스 관리 REST Api](https://msdn.microsoft.com/library/ee460799.aspx) tooadd hello AzureLogCollector 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="853a3-125">You can use [Microsoft Azure PowerShell](https://msdn.microsoft.com/library/dn495240.aspx) cmdlets or [Service Management REST APIs](https://msdn.microsoft.com/library/ee460799.aspx) tooadd hello AzureLogCollector extension.</span></span>

<span data-ttu-id="853a3-126">클라우드 서비스에 대 한 기존 Azure Powershell cmdlet을 hello **Set-azureserviceextension**, 클라우드 서비스 역할 인스턴스에서 사용 되는 tooenable hello 확장 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="853a3-126">For Cloud Services, hello existing Azure Powershell cmdlet, **Set-AzureServiceExtension**, can be used tooenable hello extension on Cloud Service role instances.</span></span> <span data-ttu-id="853a3-127">이 확장은이 cmdlet을 통해 사용 하도록 설정 될 때마다 선택 된 역할의 선택 된 hello 역할 인스턴스에서 로그 수집이 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="853a3-127">Every time this extension is enabled through this cmdlet, log collection is triggered on hello selected role instances of selected roles.</span></span>

<span data-ttu-id="853a3-128">가상 컴퓨터에 대 한 기존 Azure Powershell cmdlet을 hello **Set-azurevmextension**, 가상 컴퓨터에서 사용 되는 tooenable hello 확장 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="853a3-128">For Virtual Machines, hello existing Azure Powershell cmdlet, **Set-AzureVMExtension**, can be used tooenable hello extension on Virtual Machines.</span></span> <span data-ttu-id="853a3-129">이 확장 hello cmdlet을 통해 사용 하도록 설정 될 때마다 각 인스턴스에서 로그 수집이 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="853a3-129">Every time this extension is enabled through hello cmdlets, log collection is triggered on each instance.</span></span>

<span data-ttu-id="853a3-130">내부적으로이 확장 프로그램에서는 hello PublicConfiguration JSON 기반 및 PrivateConfiguration 합니다.</span><span class="sxs-lookup"><span data-stu-id="853a3-130">Internally, this extension uses hello JSON-based PublicConfiguration and PrivateConfiguration.</span></span> <span data-ttu-id="853a3-131">hello 다음은 공용 및 개인 구성에 대 한 샘플 JSON의 hello 레이아웃입니다.</span><span class="sxs-lookup"><span data-stu-id="853a3-131">hello following is hello layout of a sample JSON for public and private configuration.</span></span>

### <a name="publicconfiguration"></a><span data-ttu-id="853a3-132">PublicConfiguration</span><span class="sxs-lookup"><span data-stu-id="853a3-132">PublicConfiguration</span></span>
    {
        "Instances":  "*",
        "Mode":  "Full",
        "SasUri":  "SasUri tooyour storage account with sp=wl",
        "AdditionalData":
        [
          {
                  "Name":  "StorageData",
                  "Location":  "%roleroot%storage",
                  "SearchPattern":  "*.*",
                  "Recursive":  "true"
          },
          {
                "Name":  "CustomDataFolder2",
                "Location":  "c:\customFolder",
                "SearchPattern":  "*.log",
                "Recursive":  "false"
          },
        ]
    }

### <a name="privateconfiguration"></a><span data-ttu-id="853a3-133">PrivateConfiguration</span><span class="sxs-lookup"><span data-stu-id="853a3-133">PrivateConfiguration</span></span>
    {

    }

> [!NOTE]
> <span data-ttu-id="853a3-134">이 확장은 **privateConfiguration**이 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="853a3-134">This extension doesn’t need **privateConfiguration**.</span></span> <span data-ttu-id="853a3-135">Hello에 대 한 빈 구조를 제공 하기만 하면 **– PrivateConfiguration** 인수입니다.</span><span class="sxs-lookup"><span data-stu-id="853a3-135">You can just provide an empty structure for hello **–PrivateConfiguration** argument.</span></span>
> 
> 

<span data-ttu-id="853a3-136">Hello 2 중 하나를 따라 다음 단계 tooadd hello AzureLogCollector tooone 또는 클라우드 서비스 또는 가상 컴퓨터는 컬렉션에 각 VM toorun hello 트리거와 tooAzure 계정 hello 수집 된 파일을 보낼 선택 된 역할의 인스턴스 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="853a3-136">You can follow one of hello two following steps tooadd hello AzureLogCollector tooone or more instances of a Cloud Service or Virtual Machine of selected roles, which triggers hello collections on each VM toorun and send hello collected files tooAzure account specified.</span></span>

## <a name="adding-as-a-service-extension"></a><span data-ttu-id="853a3-137">서비스 확장으로 추가</span><span class="sxs-lookup"><span data-stu-id="853a3-137">Adding as a Service Extension</span></span>
1. <span data-ttu-id="853a3-138">Hello 지침 tooconnect Azure PowerShell tooyour 구독을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="853a3-138">Follow hello instructions tooconnect Azure PowerShell tooyour subscription.</span></span>
2. <span data-ttu-id="853a3-139">Hello 서비스 이름, 슬롯, 역할 및 역할 인스턴스 toowhich tooadd 원하는 하 고 hello AzureLogCollector 확장을 사용 하도록 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="853a3-139">Specify hello service name, slot, roles, and role instances toowhich you want tooadd and enable hello AzureLogCollector extension.</span></span>
   
        #Specify your cloud service name
        $ServiceName = 'extensiontest2'
   
        #Specify hello slot. 'Production' or 'Staging'
        $slot = 'Production'
   
        #Specified hello roles on which hello extension will be installed and enabled
        $roles = @("WorkerRole1","WebRole1")
   
        #Specify hello instances on which extension will be installed and enabled.  Use wildcard * for all instances
        $instances = @("*")
   
        #Specify hello collection mode, "Full" or "GA"
        $mode = "GA"
3. <span data-ttu-id="853a3-140">파일을 수집 하는 hello 추가 데이터 폴더를 지정 (이 단계는 선택 사항).</span><span class="sxs-lookup"><span data-stu-id="853a3-140">Specify hello additional data folder for which files will be collected (this step is optional).</span></span>
   
        #add one location
        $a1 = New-Object PSObject
   
        $a1 | Add-Member -MemberType NoteProperty -Name "Name" -Value "StorageData"
        $a1 | Add-Member -MemberType NoteProperty -Name "SearchPattern" -Value "*"
        $a1 | Add-Member -MemberType NoteProperty -Name "Location" -Value "%roleroot%storage"  #%roleroot% is normally E: or F: drive
        $a1 | Add-Member -MemberType NoteProperty -Name "Recursive" -Value "true"
   
        $AdditionalDataList+= $a1
              #more locations can be added....
   
   > [!NOTE]
   > <span data-ttu-id="853a3-141">토큰을 사용할 수 있습니다 `%roleroot%` 고정된 드라이브를 사용 하지 않으므로 toospecify hello 역할 루트 드라이브입니다.</span><span class="sxs-lookup"><span data-stu-id="853a3-141">You can use token `%roleroot%` toospecify hello role root drive since it doesn’t use a fixed drive.</span></span>
   > 
   > 
4. <span data-ttu-id="853a3-142">Hello Azure 저장소 계정 이름 및 키 toowhich 수집 된 파일은 업로드를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="853a3-142">Provide hello Azure storage account name and key toowhich collected files will be uploaded.</span></span>
   
        $StorageAccountName = 'YourStorageAccountName'
        $StorageAccountKey  = ‘YouStorageAccountKey'
5. <span data-ttu-id="853a3-143">클라우드 서비스에 대 한 다음과 tooenable hello AzureLogCollector 확장으로 hello SetAzureServiceLogCollector.ps1 (hello 문서의 hello 끝에 포함 됨)를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="853a3-143">Call hello SetAzureServiceLogCollector.ps1 (included at hello end of hello article) as follows tooenable hello AzureLogCollector extension for a Cloud Service.</span></span> <span data-ttu-id="853a3-144">Hello 실행이 완료 되 면 아래에 업로드 하는 hello 파일을 찾을 수 있습니다.`https://YouareStorageAccountName.blob.core.windows.net/vmlogs`</span><span class="sxs-lookup"><span data-stu-id="853a3-144">Once hello execution is completed, you can find hello uploaded file under `https://YouareStorageAccountName.blob.core.windows.net/vmlogs`</span></span>
   
        .\SetAzureServiceLogCollector.ps1 -ServiceName YourCloudServiceName  -Roles $roles  -Instances $instances –Mode $mode -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey -AdditionDataLocationList $AdditionalDataList

<span data-ttu-id="853a3-145">hello 다음은 hello 정의 toohello 스크립트를 전달 하는 hello 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="853a3-145">hello following is hello definition of hello parameters passed toohello script.</span></span> <span data-ttu-id="853a3-146">(아래에 복사됩니다.)</span><span class="sxs-lookup"><span data-stu-id="853a3-146">(This is copied below as well.)</span></span>

    [CmdletBinding(SupportsShouldProcess = $true)]

    param (
      [Parameter(Mandatory=$true)]
    [string]   $ServiceName,

    [Parameter(Mandatory=$false)]
    [string[]] $Roles ,

    [Parameter(Mandatory=$false)]
    [string[]] $Instances,

    [Parameter(Mandatory=$false)]
    [string]   $Slot = 'Production',

    [Parameter(Mandatory=$false)]
    [string]   $Mode = 'Full',

    [Parameter(Mandatory=$false)]
    [string]   $StorageAccountName,

    [Parameter(Mandatory=$false)]
    [string]   $StorageAccountKey,

    [Parameter(Mandatory=$false)]
    [PSObject[]] $AdditionDataLocationList = $null
    )

* <span data-ttu-id="853a3-147">*ServiceName*: 클라우드 서비스 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="853a3-147">*ServiceName*: Your cloud service name.</span></span>
* <span data-ttu-id="853a3-148">*역할*: "WebRole1" 또는 "WorkerRole1"과 같은 역할 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="853a3-148">*Roles*: A list of roles, such as “WebRole1” or ”WorkerRole1”.</span></span>
* <span data-ttu-id="853a3-149">*인스턴스*: 역할 인스턴스의 hello 이름의 목록을 쉼표로 구분 된 와일드 카드 문자열 hello를 사용 하세요 ("*") 모든 역할 인스턴스에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="853a3-149">*Instances*: A list of hello names of role instances separated by comma -- use hello wildcard string (“*”) for all role instances.</span></span>
* <span data-ttu-id="853a3-150">*슬롯*: 슬롯 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="853a3-150">*Slot*: Slot name.</span></span> <span data-ttu-id="853a3-151">“프로덕션” 또는 “스테이징”입니다.</span><span class="sxs-lookup"><span data-stu-id="853a3-151">“Production” or “Staging”.</span></span>
* <span data-ttu-id="853a3-152">*모드*: 컬렉션 모드입니다.</span><span class="sxs-lookup"><span data-stu-id="853a3-152">*Mode*: Collection mode.</span></span> <span data-ttu-id="853a3-153">"Full" 또는 "GA"입니다.</span><span class="sxs-lookup"><span data-stu-id="853a3-153">“Full” or “GA”.</span></span>
* <span data-ttu-id="853a3-154">*StorageAccountName*: 수집된 데이터를 저장하기 위한 Azure 저장소 계정의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="853a3-154">*StorageAccountName*: Name of Azure storage account for storing collected data.</span></span>
* <span data-ttu-id="853a3-155">*StorageAccountKey*: Azure 저장소 계정 키의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="853a3-155">*StorageAccountKey*: Name of Azure storage account key.</span></span>
* <span data-ttu-id="853a3-156">*AdditionalDataLocationList*: hello 구조를 다음 목록:</span><span class="sxs-lookup"><span data-stu-id="853a3-156">*AdditionalDataLocationList*: A list of hello following structure:</span></span>
  
      {
      String Name,
      String Location,
      String SearchPattern,
      Bool   Recursive
      }

## <a name="adding-as-a-vm-extension"></a><span data-ttu-id="853a3-157">VM 확장으로 추가</span><span class="sxs-lookup"><span data-stu-id="853a3-157">Adding as a VM Extension</span></span>
<span data-ttu-id="853a3-158">Hello 지침 tooconnect Azure PowerShell tooyour 구독을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="853a3-158">Follow hello instructions tooconnect Azure PowerShell tooyour subscription.</span></span>

1. <span data-ttu-id="853a3-159">Hello 서비스 이름, VM 및 hello 컬렉션 모드를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="853a3-159">Specify hello service name, VM, and hello collection mode.</span></span>
   
        #Specify your cloud service name
        $ServiceName = 'YourCloudServiceName'
   
        #Specify hello VM name
        $VMName = "'YourVMName'"
   
        #Specify hello collection mode, "Full" or "GA"
        $mode = "GA"
   
        Specify hello additional data folder for which files will be collected (this step is optional).
   
        #add one location
        $a1 = New-Object PSObject
   
        $a1 | Add-Member -MemberType NoteProperty -Name "Name" -Value "StorageData"
        $a1 | Add-Member -MemberType NoteProperty -Name "SearchPattern" -Value "*"
        $a1 | Add-Member -MemberType NoteProperty -Name "Location" -Value "%roleroot%storage"  #%roleroot% is normally E: or F: drive
        $a1 | Add-Member -MemberType NoteProperty -Name "Recursive" -Value "true"
   
        $AdditionalDataList+= $a1
              #more locations can be added....
2. <span data-ttu-id="853a3-160">Hello Azure 저장소 계정 이름 및 키 toowhich 수집 된 파일은 업로드를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="853a3-160">Provide hello Azure storage account name and key toowhich collected files will be uploaded.</span></span>
   
        $StorageAccountName = 'YourStorageAccountName'
        $StorageAccountKey  = ‘YouStorageAccountKey'
3. <span data-ttu-id="853a3-161">클라우드 서비스에 대 한 다음과 tooenable hello AzureLogCollector 확장으로 hello SetAzureVMLogCollector.ps1 (hello 문서의 hello 끝에 포함 됨)를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="853a3-161">Call hello SetAzureVMLogCollector.ps1 (included at hello end of hello article) as follows tooenable hello AzureLogCollector extension for a Cloud Service.</span></span> <span data-ttu-id="853a3-162">Hello 실행이 완료 되 면 https://YouareStorageAccountName.blob.core.windows.net/vmlogs hello 업로드 파일을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="853a3-162">Once hello execution is completed, you can find hello uploaded file under https://YouareStorageAccountName.blob.core.windows.net/vmlogs</span></span>

<span data-ttu-id="853a3-163">hello 다음은 hello 정의 toohello 스크립트를 전달 하는 hello 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="853a3-163">hello following is hello definition of hello parameters passed toohello script.</span></span> <span data-ttu-id="853a3-164">(아래에 복사됩니다.)</span><span class="sxs-lookup"><span data-stu-id="853a3-164">(This is copied below as well.)</span></span>

    [CmdletBinding(SupportsShouldProcess = $true)]

    param (
        [Parameter(Mandatory=$true)]
      [string]   $ServiceName,

      [Parameter(Mandatory=$false)]
      [string] $VMName ,

        [Parameter(Mandatory=$false)]
      [string]   $Mode = 'Full',

      [Parameter(Mandatory=$false)]
      [string]   $StorageAccountName,

      [Parameter(Mandatory=$false)]
      [string]   $StorageAccountKey,

      [Parameter(Mandatory=$false)]
      [PSObject[]] $AdditionDataLocationList = $null
      )

* <span data-ttu-id="853a3-165">ServiceName: 클라우드 서비스 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="853a3-165">ServiceName: Your cloud service name.</span></span>
* <span data-ttu-id="853a3-166">Hello VM의 VMName hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="853a3-166">VMName hello name of hello VM.</span></span>
* <span data-ttu-id="853a3-167">모드: 컬렉션 모드입니다.</span><span class="sxs-lookup"><span data-stu-id="853a3-167">Mode: Collection mode.</span></span> <span data-ttu-id="853a3-168">"Full" 또는 "GA"입니다.</span><span class="sxs-lookup"><span data-stu-id="853a3-168">“Full” or “GA”.</span></span>
* <span data-ttu-id="853a3-169">StorageAccountName: 수집된 데이터를 저장하기 위한 Azure 저장소 계정의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="853a3-169">StorageAccountName: Name of Azure storage account for storing collected data.</span></span>
* <span data-ttu-id="853a3-170">StorageAccountKey: Azure 저장소 계정 키의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="853a3-170">StorageAccountKey: Name of Azure storage account key.</span></span>
* <span data-ttu-id="853a3-171">AdditionalDataLocationList: hello 구조를 다음에는 목록:</span><span class="sxs-lookup"><span data-stu-id="853a3-171">AdditionalDataLocationList: A list of hello following structure:</span></span>

```
      {
        String Name,
        String Location,
        String SearchPattern,
        Bool   Recursive
      }
```

## <a name="extention-powershell-script-files"></a><span data-ttu-id="853a3-172">확장 PowerShell 스크립트 파일</span><span class="sxs-lookup"><span data-stu-id="853a3-172">Extention PowerShell Script files</span></span>
<span data-ttu-id="853a3-173">SetAzureServiceLogCollector.ps1</span><span class="sxs-lookup"><span data-stu-id="853a3-173">SetAzureServiceLogCollector.ps1</span></span>

    [CmdletBinding(SupportsShouldProcess = $true)]

    param (
                  [Parameter(Mandatory=$true)]
                  [string]   $ServiceName,

                  [Parameter(Mandatory=$false)]
                  [string[]] $Roles ,

                  [Parameter(Mandatory=$false)]
                  [string[]] $Instances = '*',

                  [Parameter(Mandatory=$false)]
                  [string]   $Slot = 'Production',

                  [Parameter(Mandatory=$false)]
                  [string]   $Mode = 'Full',

                  [Parameter(Mandatory=$false)]
                  [string]   $StorageAccountName,

                  [Parameter(Mandatory=$false)]
                  [string]   $StorageAccountKey,

                  [Parameter(Mandatory=$false)]
                  [PSObject[]] $AdditionDataLocationList = $null
            )

    $publicConfig = New-Object PSObject

    if ($Instances -ne $null -and $Instances.Count -gt 0)  #Instances should be seperated by ,
    {
        $instanceText = $Instances[0]
        for ($i = 1;$i -lt $Instances.Count;$i++)
        {
              $instanceText = $instanceText+ "," + $Instances[$i]
          }
        $publicConfig | Add-Member -MemberType NoteProperty -Name "Instances" -Value $instanceText
    }
    else  #For all instances if not specified.  hello value should be a space or *
    {
        $publicConfig | Add-Member -MemberType NoteProperty -Name "Instances" -Value " "
    }

    if ($Mode -ne $null )
    {
        $publicConfig | Add-Member -MemberType NoteProperty -Name "Mode" -Value $Mode
    }
    else
    {
        $publicConfig | Add-Member -MemberType NoteProperty -Name "Mode" -Value "Full"
    }

    #
    #we need tooget hello Sasuri from StorageAccount and containers
    #
    $context = New-AzureStorageContext -Protocol https -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

    $ContainerName = "azurelogcollectordata"
    $existingContainer = Get-AzureStorageContainer -Context $context |  Where-Object { $_.Name -like $ContainerName}
    if ($existingContainer -eq $null)
    {
        "Container ($ContainerName) doesn't exist. Creating it now.."
        New-AzureStorageContainer -Context $context -Name $ContainerName -Permission off
    }

    $ExpiryTime =  [DateTime]::Now.AddMinutes(120).ToString("o")
    $SasUri = New-AzureStorageContainerSASToken -ExpiryTime $ExpiryTime -FullUri -Name $ContainerName -Permission rwl -Context $context
    $publicConfig | Add-Member -MemberType NoteProperty -Name "SasUri" -Value $SasUri

    #
    #Add AdditionalData toocollect data from additional folders
    #
    if ($AdditionDataLocationList -ne $null )
    {
      $publicConfig | Add-Member -MemberType NoteProperty -Name "AdditionalData" -Value $AdditionDataLocationList
    }

    #
    # Convert it tooJSON format
    #
    $publicConfigJSON = $publicConfig | ConvertTo-Json
    "publicConfig is:  $publicConfigJSON"

    #we just provide a empty privateConfig object
    $privateconfig = "{
    }"

    if ($Roles -ne $null)
    {
          Set-AzureServiceExtension -Service $ServiceName -Slot $Slot -Role $Roles -ExtensionName 'AzureLogCollector' -ProviderNamespace Microsoft.WindowsAzure.Compute -PublicConfiguration $publicConfigJSON -PrivateConfiguration $privateconfig -Version 1.0 -Verbose
    }
    else
    {
          Set-AzureServiceExtension -Service $ServiceName -Slot $Slot  -ExtensionName 'AzureLogCollector' -ProviderNamespace Microsoft.WindowsAzure.Compute -PublicConfiguration $publicConfigJSON -PrivateConfiguration $privateconfig -Version 1.0 -Verbose
    }

    #
    #This is an optional step: generate a sasUri toohello container so it can be shared with other people if nened
    #
    $SasExpireTime = [DateTime]::Now.AddMinutes(120).ToString("o")
    $SasUri = New-AzureStorageContainerSASToken -ExpiryTime $ExpiryTime -FullUri -Name $ContainerName -Permission rl -Context $context
    $SasUri = $SasUri + "&restype=container&comp=list"
    Write-Output "hello container for uploaded file can be accessed using this link:`r`n$sasuri"


<span data-ttu-id="853a3-174">SetAzureVMLogCollector.ps1</span><span class="sxs-lookup"><span data-stu-id="853a3-174">SetAzureVMLogCollector.ps1</span></span>

    [CmdletBinding(SupportsShouldProcess = $true)]

    param (
                  [Parameter(Mandatory=$true)]
                  [string]   $ServiceName,

                  [Parameter(Mandatory=$false)]
                  [string] $VMName ,

                  [Parameter(Mandatory=$false)]
                  [string]   $Mode = 'Full',

                  [Parameter(Mandatory=$false)]
                  [string]   $StorageAccountName,

                  [Parameter(Mandatory=$false)]
                  [string]   $StorageAccountKey,

                  [Parameter(Mandatory=$false)]
                  [PSObject[]] $AdditionDataLocationList = $null
            )

    $publicConfig = New-Object PSObject
    $publicConfig | Add-Member -MemberType NoteProperty -Name "Instances" -Value "*"

    if ($Mode -ne $null )
    {
        $publicConfig | Add-Member -MemberType NoteProperty -Name "Mode" -Value $Mode
    }
    else
    {
        $publicConfig | Add-Member -MemberType NoteProperty -Name "Mode" -Value "Full"
    }

    #
    #we need tooget hello Sasuri from StorageAccount and containers
    #
    $context = New-AzureStorageContext -Protocol https -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

    $ContainerName = "azurelogcollectordata"
    $existingContainer = Get-AzureStorageContainer -Context $context |  Where-Object { $_.Name -like $ContainerName}
    if ($existingContainer -eq $null)
    {
        "Container ($ContainerName) doesn't exist. Creating it now.."
        New-AzureStorageContainer -Context $context -Name $ContainerName -Permission off
    }

    $ExpiryTime =  [DateTime]::Now.AddMinutes(90).ToString("o")
    $SasUri = New-AzureStorageContainerSASToken -ExpiryTime $ExpiryTime -FullUri -Name $ContainerName -Permission rwl -Context $context
    $publicConfig | Add-Member -MemberType NoteProperty -Name "SasUri" -Value $SasUri

    #
    #Add AdditionalData toocollect data from additional folders
    #
    if ($AdditionDataLocationList -ne $null )
    {
      $publicConfig | Add-Member -MemberType NoteProperty -Name "AdditionalData" -Value $AdditionDataLocationList
    }

    #
    # Convert it tooJSON format
    #
    $publicConfigJSON = $publicConfig | ConvertTo-Json

    Write-Output "PublicConfigurtion is: \r\n$publicConfigJSON"

    #
    #we just provide a empty privateConfig object
    #
    $privateconfig = "{
    }"

    if ($VMName -ne $null )
    {
          $VM = Get-AzureVM -ServiceName $ServiceName -Name $VMName
          $VM.VM.OSVirtualHardDisk.OS

          if ($VM.VM.OSVirtualHardDisk.OS -like '*Windows*')
          {
                Set-AzureVMExtension -VM $VM -ExtensionName "AzureLogCollector" -Publisher Microsoft.WindowsAzure.Compute -PublicConfiguration $publicConfigJSON -PrivateConfiguration $privateconfig -Version 1.* | Update-AzureVM -Verbose

                #
                #We will check hello VM status toofind if operation by extension has been completed or not. hello completion of hello operation,either succeed or fail, can be indicated by
                #hello presence of SubstatusList field.
                #
                $Completed = $false
                while ($Completed -ne $true)
                {
                        $VM = Get-AzureVM -ServiceName $ServiceName -Name $VMName
                        $status = $VM.ResourceExtensionStatusList | Where-Object {$_.HandlerName -eq "Microsoft.WindowsAzure.Compute.AzureLogCollector"}

                        if ( ($status.Code -ne 0) -and ($status.Status -like '*error*'))
                        {
                            Write-Output "Error status is returned: $($Status.ExtensionSettingStatus.FormattedMessage.Message)."
                              $Completed = $true
                        }
                        elseif (($status.ExtensionSettingStatus.SubstatusList -eq $null -or $status.ExtensionSettingStatus.SubstatusList.Count -lt 1))
                        {
                              $Completed = $false
                              Write-Output "Waiting for operation toocomplete..."
                        }
                        else
                        {
                              $Completed = $true
                              Write-Output "Operation completed."

                        $UploadedFileUri = $Status.ExtensionSettingStatus.SubStatusList[0].FormattedMessage.Message
                              $blob = New-Object Microsoft.WindowsAzure.Storage.Blob.CloudBlockBlob($UploadedFileUri)

                      #
                            # This is an optional step:  For easier access toohello file, we can generate a read-only SasUri directly toohello file
                              #
                              $ExpiryTimeRead =  [DateTime]::Now.AddMinutes(120).ToString("o")
                              $ReadSasUri = New-AzureStorageBlobSASToken -ExpiryTime $ExpiryTimeRead  -FullUri  -Blob  $blob.name -Container $blob.Container.Name -Permission r -Context $context

                            Write-Output "hello uploaded file can be accessed using this link: $ReadSasUri"

                              #
                              #This is an optional step:  Remove hello extension after we are done
                              #
                              Get-AzureVM -ServiceName $ServiceName -Name $VMName | Set-AzureVMExtension -Publisher Microsoft.WindowsAzure.Compute -ExtensionName "AzureLogCollector" -Version 1.* -Uninstall | Update-AzureVM -Verbose

                        }
                        Start-Sleep -s 5
                }
          }
          else
          {
              Write-Output "VM OS Type is not Windows, hello extension cannot be enabled"
          }

    }
    else
    {
      Write-Output "VM name is not specified, hello extension cannot be enabled"
    }

## <a name="next-steps"></a><span data-ttu-id="853a3-175">다음 단계</span><span class="sxs-lookup"><span data-stu-id="853a3-175">Next Steps</span></span>
<span data-ttu-id="853a3-176">이제 매우 간단한 위치에서 로그를 검사하거나 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="853a3-176">Now you can examine or copy your logs from one very simple location.</span></span>

