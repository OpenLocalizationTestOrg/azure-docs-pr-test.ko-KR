


## <a name="using-vm-extensions"></a><span data-ttu-id="dc499-101">VM 확장 사용</span><span class="sxs-lookup"><span data-stu-id="dc499-101">Using VM Extensions</span></span>
<span data-ttu-id="dc499-102">Azure VM 확장은 Azure VM의 타 프로그램 작업을 지원하거나(예: **WebDeployForVSDevTest** 확장은 Azure VM에서 Visual Studio의 웹 배포 솔루션 작업을 허용함) 일부 다른 동작을 지원하기 위해 VM과 상호 작용하는 기능을 제공(예: PowerShell, Azure CLI 및 REST 클라이언트에서 VM Access 확장을 사용하여 Azure VM에서의 원격 액세스 값을 재설정하거나 수정할 수 있음)하는 동작이나 기능을 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="dc499-102">Azure VM Extensions implement behaviors or features that either help other programs work on Azure VMs (for example, the **WebDeployForVSDevTest** extension allows Visual Studio to Web Deploy solutions on your Azure VM) or provide the ability for you to interact with the VM to support some other behavior (for example, you can use the VM Access extensions from PowerShell, the Azure CLI, and REST clients to reset or modify remote access values on your Azure VM).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="dc499-103">지원하는 기능별 전체 확장 목록은 [Azure VM 확장 및 기능](../articles/virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dc499-103">For a complete list of extensions by the features they support, see [Azure VM Extensions and Features](../articles/virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="dc499-104">각 VM 확장은 특정 기능을 지원하므로 확장에서 정확히 지원하는 기능과 지원하지 않는 기능은 확장마다 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="dc499-104">Because each VM extension supports a specific feature, exactly what you can and cannot do with an extension depends on the extension.</span></span> <span data-ttu-id="dc499-105">따라서 VM을 수정하기 전에 사용하려는 VM 확장에 대한 설명서를 읽어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc499-105">Therefore, before modifying your VM, make sure you have read the documentation for the VM Extension you want to use.</span></span> <span data-ttu-id="dc499-106">어떤 VM 확장은 제거가 지원되지 않으며 어떤 확장에서는 VM 동작을 근본적으로 변경하는 속성을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc499-106">Removing some VM Extensions is not supported; others have properties that can be set that change VM behavior radically.</span></span>
> 
> 

<span data-ttu-id="dc499-107">가장 일반적인 작업은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="dc499-107">The most common tasks are:</span></span>

1. <span data-ttu-id="dc499-108">사용 가능한 확장 찾기</span><span class="sxs-lookup"><span data-stu-id="dc499-108">Finding Available Extensions</span></span>
2. <span data-ttu-id="dc499-109">로드된 확장 업데이트</span><span class="sxs-lookup"><span data-stu-id="dc499-109">Updating Loaded Extensions</span></span>
3. <span data-ttu-id="dc499-110">확장 추가</span><span class="sxs-lookup"><span data-stu-id="dc499-110">Adding Extensions</span></span>
4. <span data-ttu-id="dc499-111">확장 제거</span><span class="sxs-lookup"><span data-stu-id="dc499-111">Removing Extensions</span></span>

## <a name="find-available-extensions"></a><span data-ttu-id="dc499-112">사용 가능한 확장 찾기</span><span class="sxs-lookup"><span data-stu-id="dc499-112">Find Available Extensions</span></span>
<span data-ttu-id="dc499-113">다음을 사용하여 확장 및 확장 정보를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc499-113">You can locate extension and extended information using:</span></span>

* <span data-ttu-id="dc499-114">PowerShell</span><span class="sxs-lookup"><span data-stu-id="dc499-114">PowerShell</span></span>
* <span data-ttu-id="dc499-115">Azure 플랫폼 간 명령줄 인터페이스(Azure CLI)</span><span class="sxs-lookup"><span data-stu-id="dc499-115">Azure Cross-Platform Command Line Interface (Azure CLI)</span></span>
* <span data-ttu-id="dc499-116">서비스 관리 REST API</span><span class="sxs-lookup"><span data-stu-id="dc499-116">Service Management REST API</span></span>

### <a name="azure-powershell"></a><span data-ttu-id="dc499-117">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="dc499-117">Azure PowerShell</span></span>
<span data-ttu-id="dc499-118">일부 확장에는 PowerShell로부터의 구성 편의를 위한 특정 PowerShell cmdlet이 있지만 다음 cmdlet은 모든 VM 확장에서 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="dc499-118">Some extensions have PowerShell cmdlets that are specific to them, which may make their configuration from PowerShell easier; but the following cmdlets work for all VM extensions.</span></span>

<span data-ttu-id="dc499-119">다음 cmdlet을 사용하여 사용 가능한 확장에 대한 정보를 구할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc499-119">You can use the following cmdlets to obtain information about available extensions:</span></span>

* <span data-ttu-id="dc499-120">웹 역할 또는 작업자 역할 인스턴스의 경우 [Get-AzureServiceAvailableExtension](https://msdn.microsoft.com/library/azure/dn722498.aspx) cmdlet을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc499-120">For instances of web roles or worker roles, you can use the [Get-AzureServiceAvailableExtension](https://msdn.microsoft.com/library/azure/dn722498.aspx) cmdlet.</span></span>
* <span data-ttu-id="dc499-121">가상 컴퓨터의 경우 [Get-AzureVMAvailableExtension](https://msdn.microsoft.com/library/azure/dn722480.aspx) cmdlet을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc499-121">For instances of Virtual Machines, you can use the [Get-AzureVMAvailableExtension](https://msdn.microsoft.com/library/azure/dn722480.aspx) cmdlet.</span></span>
  
   <span data-ttu-id="dc499-122">예를 들어, 다음 코드 예제에서는 PowerShell을 사용하여 **IaaSDiagnostics** 확장에 대한 정보를 나열하는 방법을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="dc499-122">For example, the following code example shows how to list the information for the **IaaSDiagnostics** extension using PowerShell.</span></span>
  
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

### <a name="azure-command-line-interface-azure-cli"></a><span data-ttu-id="dc499-123">Azure CLI(Azure 명령줄 인터페이스)</span><span class="sxs-lookup"><span data-stu-id="dc499-123">Azure Command Line Interface (Azure CLI)</span></span>
<span data-ttu-id="dc499-124">일부 확장에는 구성 편의를 위한 고유의 Azure CLI 명령(예: Docker VM 확장)이 있지만 다음 명령은 모든 VM 확장에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="dc499-124">Some extensions have Azure CLI commands that are specific to them (the Docker VM Extension is one example), which may make their configuration easier; but the following commands work for all VM extensions.</span></span>

<span data-ttu-id="dc499-125">**azure vm extension list** 명령을 사용하여 사용 가능한 확장에 대한 정보를 구하고 **–-json** 옵션을 사용하여 하나 이상의 확장에 대한 모든 사용 가능한 정보를 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc499-125">You can use the **azure vm extension list** command to obtain information about available extensions, and use the **–-json** option to display all available information about one or more extensions.</span></span> <span data-ttu-id="dc499-126">확장 이름을 사용하지 않는 경우 명령은 모든 사용 가능한 확장에 대해 JSON 설명을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dc499-126">If you do not use an extension name, the command returns a JSON description of all available extensions.</span></span>

<span data-ttu-id="dc499-127">예를 들어 다음 코드 예제에서는 Azure CLI **azure vm extension list** 명령을 사용하여 **IaaSDiagnostics** 확장 정보를 나열하는 방법을 보여 주고 **–-json** 옵션을 사용하여 전체 정보를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dc499-127">For example, the following code example shows how to list the information for the **IaaSDiagnostics** extension using the Azure CLI **azure vm extension list** command and uses the **–-json** option to return complete information.</span></span>

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



### <a name="service-management-rest-apis"></a><span data-ttu-id="dc499-128">서비스 관리 REST API</span><span class="sxs-lookup"><span data-stu-id="dc499-128">Service Management REST APIs</span></span>
<span data-ttu-id="dc499-129">다음 REST API를 사용하여 사용 가능한 확장에 대한 정보를 구할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc499-129">You can use the following REST APIs to obtain information about available extensions:</span></span>

* <span data-ttu-id="dc499-130">웹 역할 또는 작업자 역할 인스턴스의 경우 [사용 가능한 확장 나열](https://msdn.microsoft.com/library/dn169559.aspx) 작업을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc499-130">For instances of web roles or worker roles, you can use the [List Available Extensions](https://msdn.microsoft.com/library/dn169559.aspx) operation.</span></span> <span data-ttu-id="dc499-131">사용 가능한 확장의 버전을 나열하려면 [확장 버전 나열](https://msdn.microsoft.com/library/dn495437.aspx)을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc499-131">To list the versions of available extensions, you can use [List Extension Versions](https://msdn.microsoft.com/library/dn495437.aspx).</span></span>
* <span data-ttu-id="dc499-132">가상 컴퓨터 인스턴스의 경우 [리소스 확장 나열](https://msdn.microsoft.com/library/dn495441.aspx) 작업을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc499-132">For instances of Virtual Machines, you can use the [List Resource Extensions](https://msdn.microsoft.com/library/dn495441.aspx) operation.</span></span> <span data-ttu-id="dc499-133">사용 가능한 확장의 버전을 나열하려면 [리소스 확장 버전 나열](https://msdn.microsoft.com/library/dn495440.aspx)을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc499-133">To list the versions of available extensions, you can use [List Resource Extension Versions](https://msdn.microsoft.com/library/dn495440.aspx).</span></span>

## <a name="add-update-or-disable-extensions"></a><span data-ttu-id="dc499-134">확장 추가, 업데이트 또는 비활성화</span><span class="sxs-lookup"><span data-stu-id="dc499-134">Add, Update, or Disable Extensions</span></span>
<span data-ttu-id="dc499-135">확장은 인스턴스를 만들 때 추가하거나, 실행 중인 인스턴스에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc499-135">Extensions can be added when an instance is created or they can be added to a running instance.</span></span> <span data-ttu-id="dc499-136">확장은 업데이트, 비활성화 또는 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc499-136">Extensions can be updated, disabled, or removed.</span></span> <span data-ttu-id="dc499-137">Azure PowerShell cmdlet 또는 서비스 관리 REST API 작업을 사용하여 이러한 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc499-137">You can perform these actions by using Azure PowerShell cmdlets or by using the Service Management REST API operations.</span></span> <span data-ttu-id="dc499-138">일부 확장의 설치 및 설정에는 매개 변수가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="dc499-138">Parameters are required to install and set up some extensions.</span></span> <span data-ttu-id="dc499-139">확장에는 공용 및 개인 매개 변수가 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="dc499-139">Public and private parameters are supported for extensions.</span></span>

### <a name="azure-powershell"></a><span data-ttu-id="dc499-140">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="dc499-140">Azure PowerShell</span></span>
<span data-ttu-id="dc499-141">Azure PowerShell cmdlet을 사용하면 가장 쉽게 확장을 추가 및 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc499-141">Using Azure PowerShell cmdlets is the easiest way to add and update extensions.</span></span> <span data-ttu-id="dc499-142">확장 cmdlet을 사용하면 대부분의 확장 구성이 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="dc499-142">When you use the extension cmdlets, most of the configuration of the extension is done for you.</span></span> <span data-ttu-id="dc499-143">때때로 프로그래밍 방식으로 확장을 추가해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc499-143">At times, you may need to programmatically add an extension.</span></span> <span data-ttu-id="dc499-144">이 작업이 필요할 때는 확장의 구성을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc499-144">When you need to do this, you must provide the configuration of the extension.</span></span>

<span data-ttu-id="dc499-145">확장에서 공용 또는 개인 매개 변수 구성의 필요 여부를 파악하기 위해 다음 cmdlet을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc499-145">You can use the following cmdlets to know whether an extension requires a configuration of public and private parameters:</span></span>

* <span data-ttu-id="dc499-146">웹 역할 또는 작업자 역할 인스턴스의 경우 **Get-AzureServiceAvailableExtension** cmdlet을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc499-146">For instances of web roles or worker roles, you can use the **Get-AzureServiceAvailableExtension** cmdlet.</span></span>
* <span data-ttu-id="dc499-147">가상 컴퓨터의 경우 **Get-AzureVMAvailableExtension** cmdlet을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc499-147">For instances of Virtual Machines, you can use the **Get-AzureVMAvailableExtension** cmdlet.</span></span>

### <a name="service-management-rest-apis"></a><span data-ttu-id="dc499-148">서비스 관리 REST API</span><span class="sxs-lookup"><span data-stu-id="dc499-148">Service Management REST APIs</span></span>
<span data-ttu-id="dc499-149">REST Api를 사용하여 사용 가능한 확장 목록을 검색할 때 해당 확장이 어떻게 구성될 것인가에 대한 정보를 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dc499-149">When you retrieve a listing of available extensions by using the REST APIs, you receive information about how the extension is to be configured.</span></span> <span data-ttu-id="dc499-150">반환되는 정보는 공용 스키마와 개인 스키마에서 제시하는 매개 변수 정보를 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc499-150">The information that is returned might show parameter information represented by a public schema and private schema.</span></span> <span data-ttu-id="dc499-151">공용 매개 변수 값은 인스턴스에 대한 쿼리에서 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="dc499-151">Public parameter values are returned in queries about the instances.</span></span> <span data-ttu-id="dc499-152">개인 매개 변수 값은 반환되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dc499-152">Private parameter values are not returned.</span></span>

<span data-ttu-id="dc499-153">확장에서 공용 또는 개인 매개 변수 구성의 필요 여부를 파악하기 위해 다음 REST API를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc499-153">You can use the following REST APIs to know whether an extension requires a configuration of public and private parameters:</span></span>

* <span data-ttu-id="dc499-154">웹 역할 또는 작업자 역할 인스턴스의 경우 **PublicConfigurationSchema** 및**PrivateConfigurationSchema** 요소에 [사용 가능한 확장 나열](https://msdn.microsoft.com/library/dn169559.aspx) 작업으로부터의 응답에 있는 정보가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="dc499-154">For instances of web roles or worker roles, the **PublicConfigurationSchema** and **PrivateConfigurationSchema** elements contain the information in the response from the [List Available Extensions](https://msdn.microsoft.com/library/dn169559.aspx) operation.</span></span>
* <span data-ttu-id="dc499-155">Virtual Machines 인스턴스의 경우 **PublicConfigurationSchema** 및**PrivateConfigurationSchema** 요소에 [사용 가능한 확장 나열](https://msdn.microsoft.com/library/dn495441.aspx) 작업으로부터의 응답에 있는 정보가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="dc499-155">For instances of Virtual Machines, the **PublicConfigurationSchema** and **PrivateConfigurationSchema** elements contain the information in the response from the [List Resource Extensions](https://msdn.microsoft.com/library/dn495441.aspx) operation.</span></span>

> [!NOTE]
> <span data-ttu-id="dc499-156">확장은 JSON으로 정의된 구성을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc499-156">Extensions can also use configurations that are defined with JSON.</span></span> <span data-ttu-id="dc499-157">이러한 유형의 확장을 사용할 때는 **SampleConfig** 요소만 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="dc499-157">When these types of extensions are used, only the **SampleConfig** element is used.</span></span>
> 
> 

