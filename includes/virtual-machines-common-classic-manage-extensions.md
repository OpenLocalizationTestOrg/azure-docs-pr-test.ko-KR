


## <a name="using-vm-extensions"></a><span data-ttu-id="fd5a0-101">VM 확장 사용</span><span class="sxs-lookup"><span data-stu-id="fd5a0-101">Using VM Extensions</span></span>
<span data-ttu-id="fd5a0-102">Azure VM 확장을 동작 또는 기능 중 하나는 Azure Vm에서 작동 하는 다른 프로그램에 구현 (예를 들어 hello **WebDeployForVSDevTest** 확장을 사용 하면 Visual Studio tooWeb 배포 솔루션 Azure VM에서)를 제공 하거나 hello hello VM toosupport와 toointeract 기능이 몇 가지 다른 동작 (예를 들어 PowerShell, hello Azure CLI 및 REST 클라이언트 tooreset hello VM 액세스 확장을 사용 하거나 수정할 수 있습니다 원격 액세스 값 Azure VM에서).</span><span class="sxs-lookup"><span data-stu-id="fd5a0-102">Azure VM Extensions implement behaviors or features that either help other programs work on Azure VMs (for example, hello **WebDeployForVSDevTest** extension allows Visual Studio tooWeb Deploy solutions on your Azure VM) or provide hello ability for you toointeract with hello VM toosupport some other behavior (for example, you can use hello VM Access extensions from PowerShell, hello Azure CLI, and REST clients tooreset or modify remote access values on your Azure VM).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fd5a0-103">지 원하는 hello 기능 확장의 전체 목록은 참조 하십시오. [Azure VM 확장 및 기능](../articles/virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="fd5a0-103">For a complete list of extensions by hello features they support, see [Azure VM Extensions and Features](../articles/virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="fd5a0-104">각 VM 확장은 특정 기능을 지원 하므로 정확히 무엇 있고 확장으로 작업할 수 없는 hello 확장명에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="fd5a0-104">Because each VM extension supports a specific feature, exactly what you can and cannot do with an extension depends on hello extension.</span></span> <span data-ttu-id="fd5a0-105">따라서 VM을 수정 하기 전에 확인 hello toouse 원하는 VM 확장에 대 한 hello 설명서를 확인 하세요.</span><span class="sxs-lookup"><span data-stu-id="fd5a0-105">Therefore, before modifying your VM, make sure you have read hello documentation for hello VM Extension you want toouse.</span></span> <span data-ttu-id="fd5a0-106">어떤 VM 확장은 제거가 지원되지 않으며 어떤 확장에서는 VM 동작을 근본적으로 변경하는 속성을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd5a0-106">Removing some VM Extensions is not supported; others have properties that can be set that change VM behavior radically.</span></span>
> 
> 

<span data-ttu-id="fd5a0-107">hello 가장 일반적인 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="fd5a0-107">hello most common tasks are:</span></span>

1. <span data-ttu-id="fd5a0-108">사용 가능한 확장 찾기</span><span class="sxs-lookup"><span data-stu-id="fd5a0-108">Finding Available Extensions</span></span>
2. <span data-ttu-id="fd5a0-109">로드된 확장 업데이트</span><span class="sxs-lookup"><span data-stu-id="fd5a0-109">Updating Loaded Extensions</span></span>
3. <span data-ttu-id="fd5a0-110">확장 추가</span><span class="sxs-lookup"><span data-stu-id="fd5a0-110">Adding Extensions</span></span>
4. <span data-ttu-id="fd5a0-111">확장 제거</span><span class="sxs-lookup"><span data-stu-id="fd5a0-111">Removing Extensions</span></span>

## <a name="find-available-extensions"></a><span data-ttu-id="fd5a0-112">사용 가능한 확장 찾기</span><span class="sxs-lookup"><span data-stu-id="fd5a0-112">Find Available Extensions</span></span>
<span data-ttu-id="fd5a0-113">다음을 사용하여 확장 및 확장 정보를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd5a0-113">You can locate extension and extended information using:</span></span>

* <span data-ttu-id="fd5a0-114">PowerShell</span><span class="sxs-lookup"><span data-stu-id="fd5a0-114">PowerShell</span></span>
* <span data-ttu-id="fd5a0-115">Azure 플랫폼 간 명령줄 인터페이스(Azure CLI)</span><span class="sxs-lookup"><span data-stu-id="fd5a0-115">Azure Cross-Platform Command Line Interface (Azure CLI)</span></span>
* <span data-ttu-id="fd5a0-116">서비스 관리 REST API</span><span class="sxs-lookup"><span data-stu-id="fd5a0-116">Service Management REST API</span></span>

### <a name="azure-powershell"></a><span data-ttu-id="fd5a0-117">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="fd5a0-117">Azure PowerShell</span></span>
<span data-ttu-id="fd5a0-118">일부 확장에는 줄 수 있는 구성을 PowerShell에서 쉽게; 특정 toothem 있는 PowerShell cmdlet 하지만 hello 다음 cmdlet이 작동 모든 VM 확장에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd5a0-118">Some extensions have PowerShell cmdlets that are specific toothem, which may make their configuration from PowerShell easier; but hello following cmdlets work for all VM extensions.</span></span>

<span data-ttu-id="fd5a0-119">다음 사용 가능한 확장에 대 한 cmdlet tooobtain 정보 hello를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd5a0-119">You can use hello following cmdlets tooobtain information about available extensions:</span></span>

* <span data-ttu-id="fd5a0-120">에 대 한 인스턴스 웹 역할 또는 작업자 역할의 hello를 사용할 수 있습니다 [Get-azureserviceavailableextension](https://msdn.microsoft.com/library/azure/dn722498.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="fd5a0-120">For instances of web roles or worker roles, you can use hello [Get-AzureServiceAvailableExtension](https://msdn.microsoft.com/library/azure/dn722498.aspx) cmdlet.</span></span>
* <span data-ttu-id="fd5a0-121">에 대 한 인스턴스 가상 컴퓨터의 hello를 사용할 수 있습니다 [Get-azurevmavailableextension](https://msdn.microsoft.com/library/azure/dn722480.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="fd5a0-121">For instances of Virtual Machines, you can use hello [Get-AzureVMAvailableExtension](https://msdn.microsoft.com/library/azure/dn722480.aspx) cmdlet.</span></span>
  
   <span data-ttu-id="fd5a0-122">예를 들어, 코드 예와 방법을 다음 hello toolist hello에 대 한 정보 **IaaSDiagnostics** PowerShell을 사용 하 여 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd5a0-122">For example, hello following code example shows how toolist the information for hello **IaaSDiagnostics** extension using PowerShell.</span></span>
  
      PS C:\> Get-AzureVMAvailableExtension -ExtensionName IaaSDiagnostics
  
      Publisher                   : Microsoft.Azure.Diagnostics
      ExtensionName               : IaaSDiagnostics
      Version                     : 1.2
      Label                       : Microsoft Monitoring Agent Diagnostics
      Description                 : Microsoft Monitoring Agent Extension
      PublicConfigurationSchema   :
      PrivateConfigurationSchema  :
      IsInternalExtension         : False
      SampleConfig                :
      ReplicationCompleted        : True
      Eula                        :
      PrivacyUri                  :
      HomepageUri                 :
      IsJsonExtension             : True
      DisallowMajorVersionUpgrade : False
      SupportedOS                 :
      PublishedDate               :
      CompanyName                 :

### <a name="azure-command-line-interface-azure-cli"></a><span data-ttu-id="fd5a0-123">Azure CLI(Azure 명령줄 인터페이스)</span><span class="sxs-lookup"><span data-stu-id="fd5a0-123">Azure Command Line Interface (Azure CLI)</span></span>
<span data-ttu-id="fd5a0-124">일부 확장은 특정 toothem Azure CLI 명령에는 (hello Docker VM 확장은 한 가지 예)는 좀 더 쉽게 구성을; 하지만 hello 다음 명령이 모든 VM 확장에 대해 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd5a0-124">Some extensions have Azure CLI commands that are specific toothem (hello Docker VM Extension is one example), which may make their configuration easier; but hello following commands work for all VM extensions.</span></span>

<span data-ttu-id="fd5a0-125">Hello를 사용할 수 있습니다 **azure vm 확장 목록** 명령 사용 가능한 확장에 대 한 tooobtain 정보 및 hello를 사용 하 여 **–-json** toodisplay 하나 이상의 확장에 대 한 모든 사용 가능한 정보 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="fd5a0-125">You can use hello **azure vm extension list** command tooobtain information about available extensions, and use hello **–-json** option toodisplay all available information about one or more extensions.</span></span> <span data-ttu-id="fd5a0-126">확장 이름, 사용 하지 않는 경우 hello 명령은 사용 가능한 모든 확장에 대 한 JSON 설명을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd5a0-126">If you do not use an extension name, hello command returns a JSON description of all available extensions.</span></span>

<span data-ttu-id="fd5a0-127">예를 들어 다음 코드 예제에서는 hello toolist hello에 대 한 정보를 hello 방법을 **IaaSDiagnostics** Azure CLI hello 사용 하 여 확장 **azure vm 확장 목록** 명령을 사용 하 여 hello **–-json** tooreturn 완전 한 정보를 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="fd5a0-127">For example, hello following code example shows how toolist hello information for hello **IaaSDiagnostics** extension using hello Azure CLI **azure vm extension list** command and uses hello **–-json** option tooreturn complete information.</span></span>

    $ azure vm extension list -n IaaSDiagnostics --json
    [
      {
        "publisher": "Microsoft.Azure.Diagnostics",
        "name": "IaaSDiagnostics",
        "version": "1.2",
        "label": "Microsoft Monitoring Agent Diagnostics",
        "description": "Microsoft Monitoring Agent Extension",
        "replicationCompleted": true,
        "isJsonExtension": true
      }
    ]



### <a name="service-management-rest-apis"></a><span data-ttu-id="fd5a0-128">서비스 관리 REST API</span><span class="sxs-lookup"><span data-stu-id="fd5a0-128">Service Management REST APIs</span></span>
<span data-ttu-id="fd5a0-129">다음 사용 가능한 확장에 대 한 REST Api tooobtain 정보 hello를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd5a0-129">You can use hello following REST APIs tooobtain information about available extensions:</span></span>

* <span data-ttu-id="fd5a0-130">에 대 한 인스턴스 웹 역할 또는 작업자 역할의 hello를 사용할 수 있습니다 [사용 가능한 확장 나열](https://msdn.microsoft.com/library/dn169559.aspx) 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd5a0-130">For instances of web roles or worker roles, you can use hello [List Available Extensions](https://msdn.microsoft.com/library/dn169559.aspx) operation.</span></span> <span data-ttu-id="fd5a0-131">사용할 수 있습니다 toolist hello 버전의 사용 가능한 확장에서는 [확장 버전 나열](https://msdn.microsoft.com/library/dn495437.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="fd5a0-131">toolist hello versions of available extensions, you can use [List Extension Versions](https://msdn.microsoft.com/library/dn495437.aspx).</span></span>
* <span data-ttu-id="fd5a0-132">에 대 한 인스턴스 가상 컴퓨터의 hello를 사용할 수 있습니다 [리소스 확장 나열](https://msdn.microsoft.com/library/dn495441.aspx) 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd5a0-132">For instances of Virtual Machines, you can use hello [List Resource Extensions](https://msdn.microsoft.com/library/dn495441.aspx) operation.</span></span> <span data-ttu-id="fd5a0-133">사용할 수 있습니다 toolist hello 버전의 사용 가능한 확장에서는 [리소스 확장 버전 나열](https://msdn.microsoft.com/library/dn495440.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="fd5a0-133">toolist hello versions of available extensions, you can use [List Resource Extension Versions](https://msdn.microsoft.com/library/dn495440.aspx).</span></span>

## <a name="add-update-or-disable-extensions"></a><span data-ttu-id="fd5a0-134">확장 추가, 업데이트 또는 비활성화</span><span class="sxs-lookup"><span data-stu-id="fd5a0-134">Add, Update, or Disable Extensions</span></span>
<span data-ttu-id="fd5a0-135">인스턴스를 만들거나 인스턴스를 실행 하는 tooa 추가할 수 있습니다 때 확장을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd5a0-135">Extensions can be added when an instance is created or they can be added tooa running instance.</span></span> <span data-ttu-id="fd5a0-136">확장은 업데이트, 비활성화 또는 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd5a0-136">Extensions can be updated, disabled, or removed.</span></span> <span data-ttu-id="fd5a0-137">Azure PowerShell cmdlet을 사용 하 여 또는 hello 서비스 관리 REST API 작업을 사용 하 여 이러한 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd5a0-137">You can perform these actions by using Azure PowerShell cmdlets or by using hello Service Management REST API operations.</span></span> <span data-ttu-id="fd5a0-138">매개 변수가 필요한 tooinstall 고 일부 확장 프로그램 설정.</span><span class="sxs-lookup"><span data-stu-id="fd5a0-138">Parameters are required tooinstall and set up some extensions.</span></span> <span data-ttu-id="fd5a0-139">확장에는 공용 및 개인 매개 변수가 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="fd5a0-139">Public and private parameters are supported for extensions.</span></span>

### <a name="azure-powershell"></a><span data-ttu-id="fd5a0-140">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="fd5a0-140">Azure PowerShell</span></span>
<span data-ttu-id="fd5a0-141">Azure PowerShell cmdlet을 사용 하는 가장 쉬운 방법은 tooadd 및 업데이트 확장 hello입니다.</span><span class="sxs-lookup"><span data-stu-id="fd5a0-141">Using Azure PowerShell cmdlets is hello easiest way tooadd and update extensions.</span></span> <span data-ttu-id="fd5a0-142">Hello 확장 cmdlet을 사용 하는 경우 대부분 hello 확장의 hello 구성의은 자동으로 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd5a0-142">When you use hello extension cmdlets, most of hello configuration of hello extension is done for you.</span></span> <span data-ttu-id="fd5a0-143">때때로 할 수 있습니다 tooprogrammatically 확장을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd5a0-143">At times, you may need tooprogrammatically add an extension.</span></span> <span data-ttu-id="fd5a0-144">Toodo,이 필요한 경우 hello 확장의 hello 구성을 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd5a0-144">When you need toodo this, you must provide hello configuration of hello extension.</span></span>

<span data-ttu-id="fd5a0-145">확장에서 공용 및 개인 매개 변수를 구성 해야 하는지 여부를 cmdlet tooknow 다음 hello를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd5a0-145">You can use hello following cmdlets tooknow whether an extension requires a configuration of public and private parameters:</span></span>

* <span data-ttu-id="fd5a0-146">에 대 한 인스턴스 웹 역할 또는 작업자 역할의 hello를 사용할 수 있습니다 **Get-azureserviceavailableextension** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="fd5a0-146">For instances of web roles or worker roles, you can use hello **Get-AzureServiceAvailableExtension** cmdlet.</span></span>
* <span data-ttu-id="fd5a0-147">에 대 한 인스턴스 가상 컴퓨터의 hello를 사용할 수 있습니다 **Get-azurevmavailableextension** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="fd5a0-147">For instances of Virtual Machines, you can use hello **Get-AzureVMAvailableExtension** cmdlet.</span></span>

### <a name="service-management-rest-apis"></a><span data-ttu-id="fd5a0-148">서비스 관리 REST API</span><span class="sxs-lookup"><span data-stu-id="fd5a0-148">Service Management REST APIs</span></span>
<span data-ttu-id="fd5a0-149">Hello REST Api를 사용 하 여 사용 가능한 확장 목록을 검색 하면 hello 확장 toobe 구성 방법에 대 한 정보를 얻습니다.</span><span class="sxs-lookup"><span data-stu-id="fd5a0-149">When you retrieve a listing of available extensions by using hello REST APIs, you receive information about how hello extension is toobe configured.</span></span> <span data-ttu-id="fd5a0-150">반환 되는 hello 정보는 공용 스키마와 개인 스키마를 나타내는 매개 변수 정보를 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd5a0-150">hello information that is returned might show parameter information represented by a public schema and private schema.</span></span> <span data-ttu-id="fd5a0-151">공용 매개 변수 값은 hello 인스턴스에 대 한 쿼리에서 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fd5a0-151">Public parameter values are returned in queries about hello instances.</span></span> <span data-ttu-id="fd5a0-152">개인 매개 변수 값은 반환되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fd5a0-152">Private parameter values are not returned.</span></span>

<span data-ttu-id="fd5a0-153">확장에서 공용 및 개인 매개 변수를 구성 해야 하는지 여부를 REST Api tooknow 다음 hello를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd5a0-153">You can use hello following REST APIs tooknow whether an extension requires a configuration of public and private parameters:</span></span>

* <span data-ttu-id="fd5a0-154">에 대 한 웹 역할 또는 작업자 역할 인스턴스의 hello **PublicConfigurationSchema** 및 **PrivateConfigurationSchema** hello hello 대 한 응답으로 hello 정보를 포함 하는 요소 [목록 사용 가능한 확장](https://msdn.microsoft.com/library/dn169559.aspx) 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd5a0-154">For instances of web roles or worker roles, hello **PublicConfigurationSchema** and **PrivateConfigurationSchema** elements contain hello information in hello response from hello [List Available Extensions](https://msdn.microsoft.com/library/dn169559.aspx) operation.</span></span>
* <span data-ttu-id="fd5a0-155">에 대 한 가상 컴퓨터 인스턴스의 hello **PublicConfigurationSchema** 및 **PrivateConfigurationSchema** hello hello 대 한 응답으로 hello 정보를 포함 하는 요소 [목록 리소스 확장](https://msdn.microsoft.com/library/dn495441.aspx) 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd5a0-155">For instances of Virtual Machines, hello **PublicConfigurationSchema** and **PrivateConfigurationSchema** elements contain hello information in hello response from hello [List Resource Extensions](https://msdn.microsoft.com/library/dn495441.aspx) operation.</span></span>

> [!NOTE]
> <span data-ttu-id="fd5a0-156">확장은 JSON으로 정의된 구성을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd5a0-156">Extensions can also use configurations that are defined with JSON.</span></span> <span data-ttu-id="fd5a0-157">이러한 유형의 확장을 사용할 때만 hello **SampleConfig** 요소를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd5a0-157">When these types of extensions are used, only hello **SampleConfig** element is used.</span></span>
> 
> 

