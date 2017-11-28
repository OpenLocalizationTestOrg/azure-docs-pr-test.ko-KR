
<span data-ttu-id="cdbab-101">Microsoft Azure 클라우드 서비스로 문제 진단은 문제가 발생할 때 가상 컴퓨터에서 서비스의 로그 파일을 수집해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdbab-101">Diagnosing issues with an Microsoft Azure cloud service requires collecting the service’s log files on virtual machines as the issues occur.</span></span> <span data-ttu-id="cdbab-102">필요에 따라 AzureLogCollector 확장을 사용하여 VM에 원격으로 로그온하지 않고 웹 역할 및 작업자 역할 둘 다로 하나 이상의 클라우드 서비스 VM에서 일회성 로그 수집을 수행하고 수집한 파일을 Azure 저장소 계정으로 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdbab-102">You can use the AzureLogCollector extension on-demand to perfom one-time collection of logs from one or more Cloud Service VMs (from both web roles and worker roles) and transfer the collected files to an Azure storage account – all without remotely logging on to any of the VMs.</span></span>

> [!NOTE]
> <span data-ttu-id="cdbab-103">대부분의 로깅 기록에 대한 설명은 http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.asp에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdbab-103">Descriptions for most of the logged information can be found at http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.asp.</span></span>
> 
> 

<span data-ttu-id="cdbab-104">수집할 파일의 유형에 따라 달라지는 두 가지 모드의 컬렉션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdbab-104">There are two modes of collection dependent on the types of files to be collected.</span></span>

* <span data-ttu-id="cdbab-105">Azure 게스트 에이전트만 로그(GA).</span><span class="sxs-lookup"><span data-stu-id="cdbab-105">Azure Guest Agent Logs only (GA).</span></span> <span data-ttu-id="cdbab-106">이 컬렉션 모드는 Azure 게스트 에이전트 및 기타 Azure 구성 요소와 관련된 모든 로그를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="cdbab-106">This collection mode includes all the logs related to Azure guest agents and other Azure components.</span></span>
* <span data-ttu-id="cdbab-107">모든 로그(전체).</span><span class="sxs-lookup"><span data-stu-id="cdbab-107">All Logs (Full).</span></span> <span data-ttu-id="cdbab-108">이 컬렉션 모드는 GA 모드에서 모든 파일을 수집합니다. 또한 다음을 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="cdbab-108">This collection mode will collect all files in GA mode plus:</span></span>
  
  * <span data-ttu-id="cdbab-109">시스템 및 응용 프로그램 이벤트 로그</span><span class="sxs-lookup"><span data-stu-id="cdbab-109">system and application event logs</span></span>
  * <span data-ttu-id="cdbab-110">HTTP 오류 로그</span><span class="sxs-lookup"><span data-stu-id="cdbab-110">HTTP error logs</span></span>
  * <span data-ttu-id="cdbab-111">IIS 로그</span><span class="sxs-lookup"><span data-stu-id="cdbab-111">IIS Logs</span></span>
  * <span data-ttu-id="cdbab-112">설정 로그</span><span class="sxs-lookup"><span data-stu-id="cdbab-112">Setup logs</span></span>
  * <span data-ttu-id="cdbab-113">기타 시스템 로그</span><span class="sxs-lookup"><span data-stu-id="cdbab-113">other system logs</span></span>

<span data-ttu-id="cdbab-114">두 컬렉션 모드에서 다음 구조의 컬렉션을 사용하여 추가 데이터 수집 폴더를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdbab-114">In both collection modes, additional data collection folders can be specified by using a collection of the following structure:</span></span>

* <span data-ttu-id="cdbab-115">**이름**: 수집할 zip 파일 내의 하위 폴더의 이름으로 사용될 컬렉션의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="cdbab-115">**Name**: The name of the collection, which will be used as the name of subfolder inside the zip file to be collected.</span></span>
* <span data-ttu-id="cdbab-116">**위치**: 파일을 할당할 가상 컴퓨터의 폴더에 대한 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="cdbab-116">**Location**: The path to the folder on the virtual machine where file will be collected.</span></span>
* <span data-ttu-id="cdbab-117">**SearchPattern**: 수집할 파일의 이름 패턴입니다.</span><span class="sxs-lookup"><span data-stu-id="cdbab-117">**SearchPattern**: The pattern of the names of files to be collected.</span></span> <span data-ttu-id="cdbab-118">기본값은 “*”입니다.</span><span class="sxs-lookup"><span data-stu-id="cdbab-118">Default is “*”</span></span>
* <span data-ttu-id="cdbab-119">**재귀**: 파일을 폴더 아래에 재귀적으로 수집할지 여부입니다.</span><span class="sxs-lookup"><span data-stu-id="cdbab-119">**Recursive**: if the files will be collected recursively under the folder.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cdbab-120">필수 조건</span><span class="sxs-lookup"><span data-stu-id="cdbab-120">Prerequisites</span></span>
* <span data-ttu-id="cdbab-121">생성된 zip 파일을 저장하려면 확장에 대한 저장소 계정이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdbab-121">You need to have a storage account for extension to save generated zip files.</span></span>
* <span data-ttu-id="cdbab-122">Azure PowerShell Cmdlets V0.8.0 이상을 사용하고 있는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdbab-122">You must make sure that you are using Azure PowerShell Cmdlets V0.8.0 or above.</span></span> <span data-ttu-id="cdbab-123">자세한 내용은 [Azure 다운로드](https://azure.microsoft.com/downloads/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cdbab-123">For more information, see [Azure Downloads](https://azure.microsoft.com/downloads/).</span></span>

## <a name="add-the-extension"></a><span data-ttu-id="cdbab-124">확장 추가</span><span class="sxs-lookup"><span data-stu-id="cdbab-124">Add the extension</span></span>
<span data-ttu-id="cdbab-125">[Microsoft Azure PowerShell](https://msdn.microsoft.com/library/dn495240.aspx) cmdlet 또는 [서비스 관리 REST API](https://msdn.microsoft.com/library/ee460799.aspx)를 사용하여 AzureLogCollector 확장을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdbab-125">You can use [Microsoft Azure PowerShell](https://msdn.microsoft.com/library/dn495240.aspx) cmdlets or [Service Management REST APIs](https://msdn.microsoft.com/library/ee460799.aspx) to add the AzureLogCollector extension.</span></span>

<span data-ttu-id="cdbab-126">클라우드 서비스의 경우 기존 Azure Powershell cmdlet인 **Set-azureserviceextension**을 사용하여 클라우드 서비스 역할 인스턴스에서 확장을 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdbab-126">For Cloud Services, the existing Azure Powershell cmdlet, **Set-AzureServiceExtension**, can be used to enable the extension on Cloud Service role instances.</span></span> <span data-ttu-id="cdbab-127">이 확장이 cmdlet을 통해 사용하도록 설정될 때마다 선택한 역할의 선택한 역할 인스턴스에서 로그 수집이 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="cdbab-127">Every time this extension is enabled through this cmdlet, log collection is triggered on the selected role instances of selected roles.</span></span>

<span data-ttu-id="cdbab-128">가상 컴퓨터의 경우 기존 Azure Powershell cmdlet인 **Set-AzureVMExtension**을 사용하여 가상 컴퓨터에서 확장을 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdbab-128">For Virtual Machines, the existing Azure Powershell cmdlet, **Set-AzureVMExtension**, can be used to enable the extension on Virtual Machines.</span></span> <span data-ttu-id="cdbab-129">이 확장이 cmdlet을 통해 사용하도록 설정될 때마다 각 인스턴스에서 로그 수집이 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="cdbab-129">Every time this extension is enabled through the cmdlets, log collection is triggered on each instance.</span></span>

<span data-ttu-id="cdbab-130">내부적으로 이 확장은 JSON 기반 PublicConfiguration 및 PrivateConfiguration을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cdbab-130">Internally, this extension uses the JSON-based PublicConfiguration and PrivateConfiguration.</span></span> <span data-ttu-id="cdbab-131">다음은 공용 및 개인 구성에 대한 샘플 JSON의 레이아웃입니다.</span><span class="sxs-lookup"><span data-stu-id="cdbab-131">The following is the layout of a sample JSON for public and private configuration.</span></span>

### <a name="publicconfiguration"></a><span data-ttu-id="cdbab-132">PublicConfiguration</span><span class="sxs-lookup"><span data-stu-id="cdbab-132">PublicConfiguration</span></span>
    {
        "Instances":  "*",
        "Mode":  "Full",
        "SasUri":  "SasUri to your storage account with sp=wl",
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

### <a name="privateconfiguration"></a><span data-ttu-id="cdbab-133">PrivateConfiguration</span><span class="sxs-lookup"><span data-stu-id="cdbab-133">PrivateConfiguration</span></span>
    {

    }

> [!NOTE]
> <span data-ttu-id="cdbab-134">이 확장은 **privateConfiguration**이 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cdbab-134">This extension doesn’t need **privateConfiguration**.</span></span> <span data-ttu-id="cdbab-135">**–PrivateConfiguration** 인수에 대해 비어 있는 구조를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdbab-135">You can just provide an empty structure for the **–PrivateConfiguration** argument.</span></span>
> 
> 

<span data-ttu-id="cdbab-136">다음 두 개의 단계 중 하나를 따라 각 VM에 컬렉션을 트리거하여 지정된 Azure 계정에 수집된 파일을 실행 및 전송하는 선택한 역할의 클라우드 서비스 또는 가상 컴퓨터의 하나 이상의 인스턴스에 AzureLogCollector를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdbab-136">You can follow one of the two following steps to add the AzureLogCollector to one or more instances of a Cloud Service or Virtual Machine of selected roles, which triggers the collections on each VM to run and send the collected files to Azure account specified.</span></span>

## <a name="adding-as-a-service-extension"></a><span data-ttu-id="cdbab-137">서비스 확장으로 추가</span><span class="sxs-lookup"><span data-stu-id="cdbab-137">Adding as a Service Extension</span></span>
1. <span data-ttu-id="cdbab-138">다음 지침을 따라 구독에 Azure PowerShell을 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="cdbab-138">Follow the instructions to connect Azure PowerShell to your subscription.</span></span>
2. <span data-ttu-id="cdbab-139">AzureLogCollector 확장을 추가하고 사용하려는 서비스 이름, 슬롯, 역할 및 역할 인스턴스를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="cdbab-139">Specify the service name, slot, roles, and role instances to which you want to add and enable the AzureLogCollector extension.</span></span>
   
        #Specify your cloud service name
        $ServiceName = 'extensiontest2'
   
        #Specify the slot. 'Production' or 'Staging'
        $slot = 'Production'
   
        #Specified the roles on which the extension will be installed and enabled
        $roles = @("WorkerRole1","WebRole1")
   
        #Specify the instances on which extension will be installed and enabled.  Use wildcard * for all instances
        $instances = @("*")
   
        #Specify the collection mode, "Full" or "GA"
        $mode = "GA"
3. <span data-ttu-id="cdbab-140">수집할 파일에 대해 추가 데이터 폴더를 지정합니다(이 단계는 선택 사항).</span><span class="sxs-lookup"><span data-stu-id="cdbab-140">Specify the additional data folder for which files will be collected (this step is optional).</span></span>
   
        #add one location
        $a1 = New-Object PSObject
   
        $a1 | Add-Member -MemberType NoteProperty -Name "Name" -Value "StorageData"
        $a1 | Add-Member -MemberType NoteProperty -Name "SearchPattern" -Value "*"
        $a1 | Add-Member -MemberType NoteProperty -Name "Location" -Value "%roleroot%storage"  #%roleroot% is normally E: or F: drive
        $a1 | Add-Member -MemberType NoteProperty -Name "Recursive" -Value "true"
   
        $AdditionalDataList+= $a1
              #more locations can be added....
   
   > [!NOTE]
   > <span data-ttu-id="cdbab-141">고정된 드라이브를 사용하지 않으므로 토큰 `%roleroot%`을(를) 사용하여 역할 루트 드라이브를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdbab-141">You can use token `%roleroot%` to specify the role root drive since it doesn’t use a fixed drive.</span></span>
   > 
   > 
4. <span data-ttu-id="cdbab-142">업로드될 수집된 파일에 Azure 저장소 계정 이름 및 키를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="cdbab-142">Provide the Azure storage account name and key to which collected files will be uploaded.</span></span>
   
        $StorageAccountName = 'YourStorageAccountName'
        $StorageAccountKey  = ‘YouStorageAccountKey'
5. <span data-ttu-id="cdbab-143">클라우드 서비스에 대해 AzureLogCollector 확장을 사용하려면 다음과 같이 SetAzureServiceLogCollector.ps1(이 문서 끝에 포함됨)을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="cdbab-143">Call the SetAzureServiceLogCollector.ps1 (included at the end of the article) as follows to enable the AzureLogCollector extension for a Cloud Service.</span></span> <span data-ttu-id="cdbab-144">실행이 완료되면 `https://YouareStorageAccountName.blob.core.windows.net/vmlogs`</span><span class="sxs-lookup"><span data-stu-id="cdbab-144">Once the execution is completed, you can find the uploaded file under `https://YouareStorageAccountName.blob.core.windows.net/vmlogs`</span></span>
   
        .\SetAzureServiceLogCollector.ps1 -ServiceName YourCloudServiceName  -Roles $roles  -Instances $instances –Mode $mode -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey -AdditionDataLocationList $AdditionalDataList

<span data-ttu-id="cdbab-145">다음은 스크립트에 전달된 매개 변수의 정의입니다.</span><span class="sxs-lookup"><span data-stu-id="cdbab-145">The following is the definition of the parameters passed to the script.</span></span> <span data-ttu-id="cdbab-146">(아래에 복사됩니다.)</span><span class="sxs-lookup"><span data-stu-id="cdbab-146">(This is copied below as well.)</span></span>

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

* <span data-ttu-id="cdbab-147">*ServiceName*: 클라우드 서비스 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="cdbab-147">*ServiceName*: Your cloud service name.</span></span>
* <span data-ttu-id="cdbab-148">*역할*: "WebRole1" 또는 "WorkerRole1"과 같은 역할 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="cdbab-148">*Roles*: A list of roles, such as “WebRole1” or ”WorkerRole1”.</span></span>
* <span data-ttu-id="cdbab-149">*인스턴스*: 쉼표로 구분된 역할 인스턴스의 이름 목록입니다. 모든 역할 인스턴스에 대해 와일드카드 문자열(“*”)을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cdbab-149">*Instances*: A list of the names of role instances separated by comma -- use the wildcard string (“*”) for all role instances.</span></span>
* <span data-ttu-id="cdbab-150">*슬롯*: 슬롯 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="cdbab-150">*Slot*: Slot name.</span></span> <span data-ttu-id="cdbab-151">“프로덕션” 또는 “스테이징”입니다.</span><span class="sxs-lookup"><span data-stu-id="cdbab-151">“Production” or “Staging”.</span></span>
* <span data-ttu-id="cdbab-152">*모드*: 컬렉션 모드입니다.</span><span class="sxs-lookup"><span data-stu-id="cdbab-152">*Mode*: Collection mode.</span></span> <span data-ttu-id="cdbab-153">"Full" 또는 "GA"입니다.</span><span class="sxs-lookup"><span data-stu-id="cdbab-153">“Full” or “GA”.</span></span>
* <span data-ttu-id="cdbab-154">*StorageAccountName*: 수집된 데이터를 저장하기 위한 Azure 저장소 계정의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="cdbab-154">*StorageAccountName*: Name of Azure storage account for storing collected data.</span></span>
* <span data-ttu-id="cdbab-155">*StorageAccountKey*: Azure 저장소 계정 키의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="cdbab-155">*StorageAccountKey*: Name of Azure storage account key.</span></span>
* <span data-ttu-id="cdbab-156">*AdditionalDataLocationList*: 다음 구조의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="cdbab-156">*AdditionalDataLocationList*: A list of the following structure:</span></span>
  
      {
      String Name,
      String Location,
      String SearchPattern,
      Bool   Recursive
      }

## <a name="adding-as-a-vm-extension"></a><span data-ttu-id="cdbab-157">VM 확장으로 추가</span><span class="sxs-lookup"><span data-stu-id="cdbab-157">Adding as a VM Extension</span></span>
<span data-ttu-id="cdbab-158">다음 지침을 따라 구독에 Azure PowerShell을 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="cdbab-158">Follow the instructions to connect Azure PowerShell to your subscription.</span></span>

1. <span data-ttu-id="cdbab-159">서비스 이름, VM 및 컬렉션 모드를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="cdbab-159">Specify the service name, VM, and the collection mode.</span></span>
   
        #Specify your cloud service name
        $ServiceName = 'YourCloudServiceName'
   
        #Specify the VM name
        $VMName = "'YourVMName'"
   
        #Specify the collection mode, "Full" or "GA"
        $mode = "GA"
   
        Specify the additional data folder for which files will be collected (this step is optional).
   
        #add one location
        $a1 = New-Object PSObject
   
        $a1 | Add-Member -MemberType NoteProperty -Name "Name" -Value "StorageData"
        $a1 | Add-Member -MemberType NoteProperty -Name "SearchPattern" -Value "*"
        $a1 | Add-Member -MemberType NoteProperty -Name "Location" -Value "%roleroot%storage"  #%roleroot% is normally E: or F: drive
        $a1 | Add-Member -MemberType NoteProperty -Name "Recursive" -Value "true"
   
        $AdditionalDataList+= $a1
              #more locations can be added....
2. <span data-ttu-id="cdbab-160">업로드될 수집된 파일에 Azure 저장소 계정 이름 및 키를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="cdbab-160">Provide the Azure storage account name and key to which collected files will be uploaded.</span></span>
   
        $StorageAccountName = 'YourStorageAccountName'
        $StorageAccountKey  = ‘YouStorageAccountKey'
3. <span data-ttu-id="cdbab-161">클라우드 서비스에 대해 AzureLogCollector 확장을 사용하려면 다음과 같이 SetAzureVMLogCollector.ps1(이 문서 끝에 포함됨)을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="cdbab-161">Call the SetAzureVMLogCollector.ps1 (included at the end of the article) as follows to enable the AzureLogCollector extension for a Cloud Service.</span></span> <span data-ttu-id="cdbab-162">실행이 완료되면 업로드된 파일을 https://YouareStorageAccountName.blob.core.windows.net/vmlogs에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdbab-162">Once the execution is completed, you can find the uploaded file under https://YouareStorageAccountName.blob.core.windows.net/vmlogs</span></span>

<span data-ttu-id="cdbab-163">다음은 스크립트에 전달된 매개 변수의 정의입니다.</span><span class="sxs-lookup"><span data-stu-id="cdbab-163">The following is the definition of the parameters passed to the script.</span></span> <span data-ttu-id="cdbab-164">(아래에 복사됩니다.)</span><span class="sxs-lookup"><span data-stu-id="cdbab-164">(This is copied below as well.)</span></span>

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

* <span data-ttu-id="cdbab-165">ServiceName: 클라우드 서비스 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="cdbab-165">ServiceName: Your cloud service name.</span></span>
* <span data-ttu-id="cdbab-166">VMName: VM의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="cdbab-166">VMName The name of the VM.</span></span>
* <span data-ttu-id="cdbab-167">모드: 컬렉션 모드입니다.</span><span class="sxs-lookup"><span data-stu-id="cdbab-167">Mode: Collection mode.</span></span> <span data-ttu-id="cdbab-168">"Full" 또는 "GA"입니다.</span><span class="sxs-lookup"><span data-stu-id="cdbab-168">“Full” or “GA”.</span></span>
* <span data-ttu-id="cdbab-169">StorageAccountName: 수집된 데이터를 저장하기 위한 Azure 저장소 계정의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="cdbab-169">StorageAccountName: Name of Azure storage account for storing collected data.</span></span>
* <span data-ttu-id="cdbab-170">StorageAccountKey: Azure 저장소 계정 키의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="cdbab-170">StorageAccountKey: Name of Azure storage account key.</span></span>
* <span data-ttu-id="cdbab-171">AdditionalDataLocationList: 다음 구조의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="cdbab-171">AdditionalDataLocationList: A list of the following structure:</span></span>

```
      {
        String Name,
        String Location,
        String SearchPattern,
        Bool   Recursive
      }
```

## <a name="extention-powershell-script-files"></a><span data-ttu-id="cdbab-172">확장 PowerShell 스크립트 파일</span><span class="sxs-lookup"><span data-stu-id="cdbab-172">Extention PowerShell Script files</span></span>
<span data-ttu-id="cdbab-173">SetAzureServiceLogCollector.ps1</span><span class="sxs-lookup"><span data-stu-id="cdbab-173">SetAzureServiceLogCollector.ps1</span></span>

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
    else  #For all instances if not specified.  The value should be a space or *
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
    #we need to get the Sasuri from StorageAccount and containers
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
    #Add AdditionalData to collect data from additional folders
    #
    if ($AdditionDataLocationList -ne $null )
    {
      $publicConfig | Add-Member -MemberType NoteProperty -Name "AdditionalData" -Value $AdditionDataLocationList
    }

    #
    # Convert it to JSON format
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
    #This is an optional step: generate a sasUri to the container so it can be shared with other people if nened
    #
    $SasExpireTime = [DateTime]::Now.AddMinutes(120).ToString("o")
    $SasUri = New-AzureStorageContainerSASToken -ExpiryTime $ExpiryTime -FullUri -Name $ContainerName -Permission rl -Context $context
    $SasUri = $SasUri + "&restype=container&comp=list"
    Write-Output "The container for uploaded file can be accessed using this link:`r`n$sasuri"


<span data-ttu-id="cdbab-174">SetAzureVMLogCollector.ps1</span><span class="sxs-lookup"><span data-stu-id="cdbab-174">SetAzureVMLogCollector.ps1</span></span>

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
    #we need to get the Sasuri from StorageAccount and containers
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
    #Add AdditionalData to collect data from additional folders
    #
    if ($AdditionDataLocationList -ne $null )
    {
      $publicConfig | Add-Member -MemberType NoteProperty -Name "AdditionalData" -Value $AdditionDataLocationList
    }

    #
    # Convert it to JSON format
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
                #We will check the VM status to find if operation by extension has been completed or not. The completion of the operation,either succeed or fail, can be indicated by
                #the presence of SubstatusList field.
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
                              Write-Output "Waiting for operation to complete..."
                        }
                        else
                        {
                              $Completed = $true
                              Write-Output "Operation completed."

                        $UploadedFileUri = $Status.ExtensionSettingStatus.SubStatusList[0].FormattedMessage.Message
                              $blob = New-Object Microsoft.WindowsAzure.Storage.Blob.CloudBlockBlob($UploadedFileUri)

                      #
                            # This is an optional step:  For easier access to the file, we can generate a read-only SasUri directly to the file
                              #
                              $ExpiryTimeRead =  [DateTime]::Now.AddMinutes(120).ToString("o")
                              $ReadSasUri = New-AzureStorageBlobSASToken -ExpiryTime $ExpiryTimeRead  -FullUri  -Blob  $blob.name -Container $blob.Container.Name -Permission r -Context $context

                            Write-Output "The uploaded file can be accessed using this link: $ReadSasUri"

                              #
                              #This is an optional step:  Remove the extension after we are done
                              #
                              Get-AzureVM -ServiceName $ServiceName -Name $VMName | Set-AzureVMExtension -Publisher Microsoft.WindowsAzure.Compute -ExtensionName "AzureLogCollector" -Version 1.* -Uninstall | Update-AzureVM -Verbose

                        }
                        Start-Sleep -s 5
                }
          }
          else
          {
              Write-Output "VM OS Type is not Windows, the extension cannot be enabled"
          }

    }
    else
    {
      Write-Output "VM name is not specified, the extension cannot be enabled"
    }

## <a name="next-steps"></a><span data-ttu-id="cdbab-175">다음 단계</span><span class="sxs-lookup"><span data-stu-id="cdbab-175">Next Steps</span></span>
<span data-ttu-id="cdbab-176">이제 매우 간단한 위치에서 로그를 검사하거나 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdbab-176">Now you can examine or copy your logs from one very simple location.</span></span>

