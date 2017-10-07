---
title: "PowerShell을 사용 하 여 Azure 클라우드 서비스에서 aaaEnable 진단 | Microsoft Docs"
description: "PowerShell을 사용 하 여 클라우드에 대 한 tooenable 진단을 서비스 하는 방법에 대해 알아봅니다"
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: 66e08754-8639-4022-ae18-4237749ba17d
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 09/06/2016
ms.author: adegeo
ms.openlocfilehash: 7c7444df13edc8d7f5663e20ec7558d36aac45d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-diagnostics-in-azure-cloud-services-using-powershell"></a><span data-ttu-id="8d9d8-103">PowerShell을 사용하여 Azure 클라우드 서비스에 진단 사용</span><span class="sxs-lookup"><span data-stu-id="8d9d8-103">Enable diagnostics in Azure Cloud Services using PowerShell</span></span>
<span data-ttu-id="8d9d8-104">응용 프로그램 로그와 같은 진단 데이터를 수집할 수 있습니다, 성능 카운터 사용 하 여 클라우드 서비스 등 hello Azure 진단 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d9d8-104">You can collect diagnostic data like application logs, performance counters etc. from a Cloud Service using hello Azure Diagnostics extension.</span></span> <span data-ttu-id="8d9d8-105">이 문서에서는 tooenable PowerShell을 사용 하 여 클라우드 서비스에 대 한 Azure 진단 확장을 hello 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d9d8-105">This article describes how tooenable hello Azure Diagnostics extension for a Cloud Service using PowerShell.</span></span>  <span data-ttu-id="8d9d8-106">참조 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview) hello이이 문서에 필요한 필수 구성 요소에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d9d8-106">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for hello prerequisites needed for this article.</span></span>

## <a name="enable-diagnostics-extension-as-part-of-deploying-a-cloud-service"></a><span data-ttu-id="8d9d8-107">클라우드 서비스 배포의 일부로 진단 확장을 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="8d9d8-107">Enable diagnostics extension as part of deploying a Cloud Service</span></span>
<span data-ttu-id="8d9d8-108">이 방법은 시나리오, 여기서 hello 진단 확장을 배포의 일부로 사용할 수 있습니다 hello 클라우드 서비스의 적용 가능한 toocontinuous 통합 형식에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d9d8-108">This approach is applicable toocontinuous integration type of scenarios, where hello diagnostics extension can be enabled as part of deploying hello cloud service.</span></span> <span data-ttu-id="8d9d8-109">새 클라우드 서비스 배포를 만들 때 hello 전달 하 여 hello 진단 확장을 사용할 수 있습니다 *ExtensionConfiguration* 매개 변수 toohello [새로 AzureDeployment](/powershell/module/azure/new-azuredeployment?view=azuresmps-3.7.0) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="8d9d8-109">When creating a new Cloud Service deployment you can enable hello diagnostics extension by passing in hello *ExtensionConfiguration* parameter toohello [New-AzureDeployment](/powershell/module/azure/new-azuredeployment?view=azuresmps-3.7.0) cmdlet.</span></span> <span data-ttu-id="8d9d8-110">hello *ExtensionConfiguration* 매개 변수는 hello를 사용 하 여 만들 수 있는 진단 구성의 배열을 [새로 AzureServiceDiagnosticsExtensionConfig](/powershell/module/azure/new-azureservicediagnosticsextensionconfig?view=azuresmps-3.7.0) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="8d9d8-110">hello *ExtensionConfiguration* parameter takes an array of diagnostics configurations that can be created using hello [New-AzureServiceDiagnosticsExtensionConfig](/powershell/module/azure/new-azureservicediagnosticsextensionconfig?view=azuresmps-3.7.0) cmdlet.</span></span>

<span data-ttu-id="8d9d8-111">hello 다음 예제에서는 WebRole 및 WorkerRole 각 더 여러 진단 구성을 사용 하 여 클라우드 서비스에 대 한 진단을 설정 하는 방법</span><span class="sxs-lookup"><span data-stu-id="8d9d8-111">hello following example shows how you can enable diagnostics for a cloud service with a WebRole and WorkerRole, each having a different diagnostics configuration.</span></span>

```powershell
$service_name = "MyService"
$service_package = "CloudService.cspkg"
$service_config = "ServiceConfiguration.Cloud.cscfg"
$webrole_diagconfigpath = "MyService.WebRole.PubConfig.xml"
$workerrole_diagconfigpath = "MyService.WorkerRole.PubConfig.xml"

$webrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WebRole" -DiagnosticsConfigurationPath $webrole_diagconfigpath
$workerrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WorkerRole" -DiagnosticsConfigurationPath $workerrole_diagconfigpath

New-AzureDeployment -ServiceName $service_name -Slot Production -Package $service_package -Configuration $service_config -ExtensionConfiguration @($webrole_diagconfig,$workerrole_diagconfig)
```

<span data-ttu-id="8d9d8-112">Hello 진단 구성 파일을 지정 하는 경우는 `StorageAccount` 저장소 계정 이름 가진 요소가 다음 hello `New-AzureServiceDiagnosticsExtensionConfig` cmdlet에는 해당 저장소 계정을 자동으로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8d9d8-112">If hello diagnostics configuration file specifies a `StorageAccount` element with a storage account name, then hello `New-AzureServiceDiagnosticsExtensionConfig` cmdlet will automatically use that storage account.</span></span> <span data-ttu-id="8d9d8-113">이 toowork hello 저장소 계정이 필요 합니다. toobe에 클라우드 서비스가 배포 되 고 hello으로 동일한 구독 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d9d8-113">For this toowork, hello storage account needs toobe in hello same subscription as hello Cloud Service being deployed.</span></span>

<span data-ttu-id="8d9d8-114">Hello MSBuild에 의해 생성 된 향후 hello 확장 구성 파일을 게시 하는 Azure SDK 2.6에서 대상 출력 hello 서비스 구성 파일 (.cscfg)에 지정 된 hello 진단 구성 문자열을 기반으로 hello 저장소 계정 이름이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8d9d8-114">From Azure SDK 2.6 onward hello extension configuration files generated by hello MSBuild publish target output will include hello storage account name based on hello diagnostics configuration string specified in hello service configuration file (.cscfg).</span></span> <span data-ttu-id="8d9d8-115">아래의 hello 스크립트 hello에서 tooparse hello 확장 구성 파일 대상 출력을 게시 하 고 hello 클라우드 서비스를 배포 하는 경우 각 역할에 대해 진단 확장을 구성 하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="8d9d8-115">hello script below shows you how tooparse hello Extension configuration files from hello publish target output and configure diagnostics extension for each role when deploying hello cloud service.</span></span>

```powershell
$service_name = "MyService"
$service_package = "C:\build\output\CloudService.cspkg"
$service_config = "C:\build\output\ServiceConfiguration.Cloud.cscfg"

#Find hello Extensions path based on service configuration file
$extensionsSearchPath = Join-Path -Path (Split-Path -Parent $service_config) -ChildPath "Extensions"

$diagnosticsExtensions = Get-ChildItem -Path $extensionsSearchPath -Filter "PaaSDiagnostics.*.PubConfig.xml"
$diagnosticsConfigurations = @()
foreach ($extPath in $diagnosticsExtensions)
{
    #Find hello RoleName based on file naming convention PaaSDiagnostics.<RoleName>.PubConfig.xml
    $roleName = ""
    $roles = $extPath -split ".",0,"simplematch"
    if ($roles -is [system.array] -and $roles.Length -gt 1)
    {
        $roleName = $roles[1]
        $x = 2
        while ($x -le $roles.Length)
            {
               if ($roles[$x] -ne "PubConfig")
                {
                    $roleName = $roleName + "." + $roles[$x]
                }
                else
                {
                    break
                }
                $x++
            }
        $fullExtPath = Join-Path -path $extensionsSearchPath -ChildPath $extPath
        $diagnosticsconfig = New-AzureServiceDiagnosticsExtensionConfig -Role $roleName -DiagnosticsConfigurationPath $fullExtPath
        $diagnosticsConfigurations += $diagnosticsconfig
    }
}
New-AzureDeployment -ServiceName $service_name -Slot Production -Package $service_package -Configuration $service_config -ExtensionConfiguration $diagnosticsConfigurations
```

<span data-ttu-id="8d9d8-116">Visual Studio Online hello 진단 확장이 적용 된 클라우드 서비스의 자동화 된 배포 유사한 방법을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8d9d8-116">Visual Studio Online uses a similar approach for automated deployments of Cloud Services with hello diagnostics extension.</span></span> <span data-ttu-id="8d9d8-117">전체 예제는 [Publish-AzureCloudDeployment.ps1](https://github.com/Microsoft/vso-agent-tasks/blob/master/Tasks/AzureCloudPowerShellDeployment/Publish-AzureCloudDeployment.ps1) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8d9d8-117">See [Publish-AzureCloudDeployment.ps1](https://github.com/Microsoft/vso-agent-tasks/blob/master/Tasks/AzureCloudPowerShellDeployment/Publish-AzureCloudDeployment.ps1) for a complete example.</span></span>

<span data-ttu-id="8d9d8-118">없는 경우 `StorageAccount` hello에 toopass 필요 hello 진단 구성에 지정 된 *StorageAccountName* toohello cmdlet 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="8d9d8-118">If no `StorageAccount` was specified in hello diagnostics configuration, then you need toopass in hello *StorageAccountName* parameter toohello cmdlet.</span></span> <span data-ttu-id="8d9d8-119">경우 hello *StorageAccountName* hello cmdlet은 항상 hello 매개 변수에서 지정 된 hello 저장소 계정을 사용 하 여를 하지 hello 하나 hello 진단 구성 파일에 지정 된 다음 매개 변수를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d9d8-119">If hello *StorageAccountName* parameter is specified, then hello cmdlet will always use hello storage account that is specified in hello parameter and not hello one that is specified in hello diagnostics configuration file.</span></span>

<span data-ttu-id="8d9d8-120">Hello의 hello 진단 저장소 계정 tooexplicitly 필요 hello 클라우드 서비스에서에서 다른 구독에는 통과 하면 *StorageAccountName* 및 *StorageAccountKey* 매개 변수 toohello cmdlet을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d9d8-120">If hello diagnostics storage account is in a different subscription from hello Cloud Service, then you need tooexplicitly pass in hello *StorageAccountName* and *StorageAccountKey* parameters toohello cmdlet.</span></span> <span data-ttu-id="8d9d8-121">hello *StorageAccountKey* 자동으로 쿼리 하 고 hello 진단 확장을 사용 하도록 설정할 때 hello 키 값을 설정할 수 hello cmdlet으로 hello 진단 저장소 계정이 동일한 구독을 hello 매개 변수가 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8d9d8-121">hello *StorageAccountKey* parameter is not needed when hello diagnostics storage account is in hello same subscription, as hello cmdlet can automatically query and set hello key value when enabling hello diagnostics extension.</span></span> <span data-ttu-id="8d9d8-122">그러나 hello 진단 저장소 계정이 다른 구독에는 hello cmdlet 하지 못할 수 tooget hello 키 자동으로 고 tooexplicitly 필요한 hello 통해 hello 키 지정 *StorageAccountKey* 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="8d9d8-122">However, if hello diagnostics storage account is in a different subscription, then hello cmdlet might not be able tooget hello key automatically and you need tooexplicitly specify hello key through hello *StorageAccountKey* parameter.</span></span>

```powershell
$webrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WebRole" -DiagnosticsConfigurationPath $webrole_diagconfigpath -StorageAccountName $diagnosticsstorage_name -StorageAccountKey $diagnosticsstorage_key
$workerrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WorkerRole" -DiagnosticsConfigurationPath $workerrole_diagconfigpath -StorageAccountName $diagnosticsstorage_name -StorageAccountKey $diagnosticsstorage_key
```

## <a name="enable-diagnostics-extension-on-an-existing-cloud-service"></a><span data-ttu-id="8d9d8-123">기존 클라우드 서비스에 진단 확장을 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="8d9d8-123">Enable diagnostics extension on an existing Cloud Service</span></span>
<span data-ttu-id="8d9d8-124">Hello를 사용할 수 있습니다 [집합 AzureServiceDiagnosticsExtension](/powershell/module/azure/set-azureservicediagnosticsextension?view=azuresmps-3.7.0) 이미 실행 중인 클라우드 서비스에서 cmdlet tooenable 또는 업데이트 진단 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d9d8-124">You can use hello [Set-AzureServiceDiagnosticsExtension](/powershell/module/azure/set-azureservicediagnosticsextension?view=azuresmps-3.7.0) cmdlet tooenable or update diagnostics configuration on a Cloud Service that is already running.</span></span>

[!INCLUDE [cloud-services-wad-warning](../../includes/cloud-services-wad-warning.md)]

```powershell
$service_name = "MyService"
$webrole_diagconfigpath = "MyService.WebRole.PubConfig.xml"
$workerrole_diagconfigpath = "MyService.WorkerRole.PubConfig.xml"

$webrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WebRole" -DiagnosticsConfigurationPath $webrole_diagconfigpath
$workerrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WorkerRole" -DiagnosticsConfigurationPath $workerrole_diagconfigpath

Set-AzureServiceDiagnosticsExtension -DiagnosticsConfiguration @($webrole_diagconfig,$workerrole_diagconfig) -ServiceName $service_name
```

## <a name="get-current-diagnostics-extension-configuration"></a><span data-ttu-id="8d9d8-125">현재 진단 확장 구성 가져오기</span><span class="sxs-lookup"><span data-stu-id="8d9d8-125">Get current diagnostics extension configuration</span></span>
<span data-ttu-id="8d9d8-126">사용 하 여 hello [Get AzureServiceDiagnosticsExtension](/powershell/module/azure/get-azureservicediagnosticsextension?view=azuresmps-3.7.0) 클라우드 서비스에 대 한 cmdlet tooget hello 현재 진단 구성을 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d9d8-126">Use hello [Get-AzureServiceDiagnosticsExtension](/powershell/module/azure/get-azureservicediagnosticsextension?view=azuresmps-3.7.0) cmdlet tooget hello current diagnostics configuration for a cloud service.</span></span>

```powershell
Get-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```

## <a name="remove-diagnostics-extension"></a><span data-ttu-id="8d9d8-127">진단 확장 제거</span><span class="sxs-lookup"><span data-stu-id="8d9d8-127">Remove diagnostics extension</span></span>
<span data-ttu-id="8d9d8-128">서비스는 클라우드에 대 한 진단 유틸리티 오프 tooturn hello צ ְ ײ [제거 AzureServiceDiagnosticsExtension](/powershell/module/azure/remove-azureservicediagnosticsextension?view=azuresmps-3.7.0) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="8d9d8-128">tooturn off diagnostics on a cloud service you can use hello [Remove-AzureServiceDiagnosticsExtension](/powershell/module/azure/remove-azureservicediagnosticsextension?view=azuresmps-3.7.0) cmdlet.</span></span>

```powershell
Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```

<span data-ttu-id="8d9d8-129">중 하나를 사용 하 여 hello 진단 확장을 사용 하는 경우 *집합 AzureServiceDiagnosticsExtension* 또는 hello *새로 AzureServiceDiagnosticsExtensionConfig* hello 없이 *역할* 다음 매개 변수 사용 하 여 hello 확장을 제거할 수 *제거 AzureServiceDiagnosticsExtension* hello 없이 *역할* 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="8d9d8-129">If you enabled hello diagnostics extension using either *Set-AzureServiceDiagnosticsExtension* or hello *New-AzureServiceDiagnosticsExtensionConfig* without hello *Role* parameter then you can remove hello extension using *Remove-AzureServiceDiagnosticsExtension* without hello *Role* parameter.</span></span> <span data-ttu-id="8d9d8-130">경우 hello *역할* 이면 hello 확장을 사용 하도록 설정 해야 경우에 사용할 hello 확장명을 제거 하는 경우 매개 변수가 사용 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="8d9d8-130">If hello *Role* parameter was used when enabling hello extension then it must also be used when removing hello extension.</span></span>

<span data-ttu-id="8d9d8-131">각 개별 역할에서 tooremove hello 진단 확장:</span><span class="sxs-lookup"><span data-stu-id="8d9d8-131">tooremove hello diagnostics extension from each individual role:</span></span>

```powershell
Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService" -Role "WebRole"
```

## <a name="next-steps"></a><span data-ttu-id="8d9d8-132">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8d9d8-132">Next Steps</span></span>
* <span data-ttu-id="8d9d8-133">Azure 진단 및 기타 기술 tootroubleshoot 문제 사용에 대 한 추가 지침을 참조 하십시오. [Azure 클라우드 서비스 및 가상 컴퓨터에서 진단 사용](cloud-services-dotnet-diagnostics.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8d9d8-133">For additional guidance on using Azure diagnostics and other techniques tootroubleshoot problems, see [Enabling Diagnostics in Azure Cloud Services and Virtual Machines](cloud-services-dotnet-diagnostics.md).</span></span>
* <span data-ttu-id="8d9d8-134">hello [진단 구성 스키마](https://msdn.microsoft.com/library/azure/dn782207.aspx) hello hello 진단 확장에 대 한 다양 한 xml 구성 옵션에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d9d8-134">hello [Diagnostics Configuration Schema](https://msdn.microsoft.com/library/azure/dn782207.aspx) explains hello various xml configurations options for hello diagnostics extension.</span></span>
* <span data-ttu-id="8d9d8-135">tooenable hello 진단 확장 가상 컴퓨터에 대 한 참조 toolearn [모니터링 및 Azure 리소스 관리자 템플릿을 사용 하 여 진단을 사용 하 여 Windows 가상 컴퓨터 만들기](../virtual-machines/windows/extensions-diagnostics-template.md)</span><span class="sxs-lookup"><span data-stu-id="8d9d8-135">toolearn how tooenable hello diagnostics extension for Virtual Machines, see [Create a Windows Virtual machine with monitoring and diagnostics using Azure Resource Manager Template](../virtual-machines/windows/extensions-diagnostics-template.md)</span></span>
