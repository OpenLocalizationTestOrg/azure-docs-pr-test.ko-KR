---
title: "PowerShell을 사용하여 Azure 클라우드 서비스에 진단 사용 | Microsoft Docs"
description: "PowerShell을 사용하여 클라우드 서비스에 진단을 사용하도록 설정하는 방법을 알아봅니다."
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
ms.openlocfilehash: 8dd9724981860c9cd4ccc443cc2bfdc465811e7c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="enable-diagnostics-in-azure-cloud-services-using-powershell"></a><span data-ttu-id="48e41-103">PowerShell을 사용하여 Azure 클라우드 서비스에 진단 사용</span><span class="sxs-lookup"><span data-stu-id="48e41-103">Enable diagnostics in Azure Cloud Services using PowerShell</span></span>
<span data-ttu-id="48e41-104">Azure 진단 확장을 사용하여 클라우드 서비스로부터 응용 프로그램 로그, 성능 카운터 등과 같은 진단 데이터를 수집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48e41-104">You can collect diagnostic data like application logs, performance counters etc. from a Cloud Service using the Azure Diagnostics extension.</span></span> <span data-ttu-id="48e41-105">이 문서는 PowerShell을 사용하여 클라우드 서비스에 대해 Azure 진단 확장을 사용하도록 설정하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="48e41-105">This article describes how to enable the Azure Diagnostics extension for a Cloud Service using PowerShell.</span></span>  <span data-ttu-id="48e41-106">이 문서에 요구되는 필수 조건은 [Azure PowerShell 설치 및 구성하는 방법](/powershell/azure/overview) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="48e41-106">See [How to install and configure Azure PowerShell](/powershell/azure/overview) for the prerequisites needed for this article.</span></span>

## <a name="enable-diagnostics-extension-as-part-of-deploying-a-cloud-service"></a><span data-ttu-id="48e41-107">클라우드 서비스 배포의 일부로 진단 확장을 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="48e41-107">Enable diagnostics extension as part of deploying a Cloud Service</span></span>
<span data-ttu-id="48e41-108">이 접근 방식은 진단 확장이 클라우드 서비스의 배포 중 일부로 사용될 수 있는 연속 통합 형식의 시나리오에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="48e41-108">This approach is applicable to continuous integration type of scenarios, where the diagnostics extension can be enabled as part of deploying the cloud service.</span></span> <span data-ttu-id="48e41-109">새 클라우드 서비스 배포를 만들 경우 *ExtensionConfiguration* 매개 변수에서 [New-AzureDeployment](/powershell/module/azure/new-azuredeployment?view=azuresmps-3.7.0) cmdlet으로 전달하여 진단 확장을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48e41-109">When creating a new Cloud Service deployment you can enable the diagnostics extension by passing in the *ExtensionConfiguration* parameter to the [New-AzureDeployment](/powershell/module/azure/new-azuredeployment?view=azuresmps-3.7.0) cmdlet.</span></span> <span data-ttu-id="48e41-110">*ExtensionConfiguration* 매개 변수는 [New-AzureServiceDiagnosticsExtensionConfig](/powershell/module/azure/new-azureservicediagnosticsextensionconfig?view=azuresmps-3.7.0) cmdlet을 사용하여 만들 수 있는 진단 구성 배열을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="48e41-110">The *ExtensionConfiguration* parameter takes an array of diagnostics configurations that can be created using the [New-AzureServiceDiagnosticsExtensionConfig](/powershell/module/azure/new-azureservicediagnosticsextensionconfig?view=azuresmps-3.7.0) cmdlet.</span></span>

<span data-ttu-id="48e41-111">다음 예제는 각각 진단 구성이 다른 WebRole 및 WorkerRole을 사용하여 클라우드 서비스에 대해 진단을 사용하도록 설정하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="48e41-111">The following example shows how you can enable diagnostics for a cloud service with a WebRole and WorkerRole, each having a different diagnostics configuration.</span></span>

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

<span data-ttu-id="48e41-112">진단 구성 파일이 저장소 계정 이름으로 `StorageAccount` 요소를 지정할 경우 `New-AzureServiceDiagnosticsExtensionConfig` cmdlet에서 해당 저장소 계정을 자동으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="48e41-112">If the diagnostics configuration file specifies a `StorageAccount` element with a storage account name, then the `New-AzureServiceDiagnosticsExtensionConfig` cmdlet will automatically use that storage account.</span></span> <span data-ttu-id="48e41-113">이렇게 작동하려면, 저장소 계정이 배포된 클라우드 서비스와 동일한 구독에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="48e41-113">For this to work, the storage account needs to be in the same subscription as the Cloud Service being deployed.</span></span>

<span data-ttu-id="48e41-114">Azure SDK 2.6 이후부터 MSBuild 게시 대상 출력에 의해 생성된 확장 구성 파일은 서비스 구성 파일(.cscfg)에 지정된 진단 구성 문자열에 기반한 저장소 계정 이름을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="48e41-114">From Azure SDK 2.6 onward the extension configuration files generated by the MSBuild publish target output will include the storage account name based on the diagnostics configuration string specified in the service configuration file (.cscfg).</span></span> <span data-ttu-id="48e41-115">아래의 스크립트에서는 게시 대상 출력에서 확장 구성 파일을 구문 분석하고 클라우드 서비스를 배포할 때 각 역할에 대한 진단 확장을 구성하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="48e41-115">The script below shows you how to parse the Extension configuration files from the publish target output and configure diagnostics extension for each role when deploying the cloud service.</span></span>

```powershell
$service_name = "MyService"
$service_package = "C:\build\output\CloudService.cspkg"
$service_config = "C:\build\output\ServiceConfiguration.Cloud.cscfg"

#Find the Extensions path based on service configuration file
$extensionsSearchPath = Join-Path -Path (Split-Path -Parent $service_config) -ChildPath "Extensions"

$diagnosticsExtensions = Get-ChildItem -Path $extensionsSearchPath -Filter "PaaSDiagnostics.*.PubConfig.xml"
$diagnosticsConfigurations = @()
foreach ($extPath in $diagnosticsExtensions)
{
    #Find the RoleName based on file naming convention PaaSDiagnostics.<RoleName>.PubConfig.xml
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

<span data-ttu-id="48e41-116">Visual Studio Online은 진단 확장으로 클라우드 서비스의 자동화된 배포에 대해 유사한 접근 방식을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="48e41-116">Visual Studio Online uses a similar approach for automated deployments of Cloud Services with the diagnostics extension.</span></span> <span data-ttu-id="48e41-117">전체 예제는 [Publish-AzureCloudDeployment.ps1](https://github.com/Microsoft/vso-agent-tasks/blob/master/Tasks/AzureCloudPowerShellDeployment/Publish-AzureCloudDeployment.ps1) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="48e41-117">See [Publish-AzureCloudDeployment.ps1](https://github.com/Microsoft/vso-agent-tasks/blob/master/Tasks/AzureCloudPowerShellDeployment/Publish-AzureCloudDeployment.ps1) for a complete example.</span></span>

<span data-ttu-id="48e41-118">진단 구성에 `StorageAccount`가 지정되지 않은 경우 cmdlet에 *StorageAccountName* 매개 변수를 전달해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="48e41-118">If no `StorageAccount` was specified in the diagnostics configuration, then you need to pass in the *StorageAccountName* parameter to the cmdlet.</span></span> <span data-ttu-id="48e41-119">*StorageAccountName* 매개 변수가 지정된 경우 cmdlet은 항상 진단 구성 파일에 지정된 저장소 계정이 아닌 매개 변수에 지정된 저장소 계정을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="48e41-119">If the *StorageAccountName* parameter is specified, then the cmdlet will always use the storage account that is specified in the parameter and not the one that is specified in the diagnostics configuration file.</span></span>

<span data-ttu-id="48e41-120">진단 저장소 계정이 클라우드 서비스와 다른 구독에 있는 경우 *StorageAccountName* 및 *StorageAccountKey* 매개 변수를 cmdlet에 명시적으로 전달해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="48e41-120">If the diagnostics storage account is in a different subscription from the Cloud Service, then you need to explicitly pass in the *StorageAccountName* and *StorageAccountKey* parameters to the cmdlet.</span></span> <span data-ttu-id="48e41-121">진단 저장소 계정이 동일한 구독에 있는 경우 진단 확장을 사용하도록 설정하면 cmdlet이 키 값을 자동으로 쿼리하고 설정할 수 있으므로 *StorageAccountKey* 매개 변수가 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="48e41-121">The *StorageAccountKey* parameter is not needed when the diagnostics storage account is in the same subscription, as the cmdlet can automatically query and set the key value when enabling the diagnostics extension.</span></span> <span data-ttu-id="48e41-122">하지만 진단 저장소 계정이 다른 구독에 있는 경우에는 cmdlet이 자동으로 키를 얻지 못할 수 있으며, 사용자가 *StorageAccountKey* 매개 변수를 통해 키를 명시적으로 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="48e41-122">However, if the diagnostics storage account is in a different subscription, then the cmdlet might not be able to get the key automatically and you need to explicitly specify the key through the *StorageAccountKey* parameter.</span></span>

```powershell
$webrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WebRole" -DiagnosticsConfigurationPath $webrole_diagconfigpath -StorageAccountName $diagnosticsstorage_name -StorageAccountKey $diagnosticsstorage_key
$workerrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WorkerRole" -DiagnosticsConfigurationPath $workerrole_diagconfigpath -StorageAccountName $diagnosticsstorage_name -StorageAccountKey $diagnosticsstorage_key
```

## <a name="enable-diagnostics-extension-on-an-existing-cloud-service"></a><span data-ttu-id="48e41-123">기존 클라우드 서비스에 진단 확장을 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="48e41-123">Enable diagnostics extension on an existing Cloud Service</span></span>
<span data-ttu-id="48e41-124">[Set-AzureServiceDiagnosticsExtension](/powershell/module/azure/set-azureservicediagnosticsextension?view=azuresmps-3.7.0) cmdlet을 사용하여 이미 실행 중인 클라우드 서비스에 진단 구성을 사용하거나 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48e41-124">You can use the [Set-AzureServiceDiagnosticsExtension](/powershell/module/azure/set-azureservicediagnosticsextension?view=azuresmps-3.7.0) cmdlet to enable or update diagnostics configuration on a Cloud Service that is already running.</span></span>

[!INCLUDE [cloud-services-wad-warning](../../includes/cloud-services-wad-warning.md)]

```powershell
$service_name = "MyService"
$webrole_diagconfigpath = "MyService.WebRole.PubConfig.xml"
$workerrole_diagconfigpath = "MyService.WorkerRole.PubConfig.xml"

$webrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WebRole" -DiagnosticsConfigurationPath $webrole_diagconfigpath
$workerrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WorkerRole" -DiagnosticsConfigurationPath $workerrole_diagconfigpath

Set-AzureServiceDiagnosticsExtension -DiagnosticsConfiguration @($webrole_diagconfig,$workerrole_diagconfig) -ServiceName $service_name
```

## <a name="get-current-diagnostics-extension-configuration"></a><span data-ttu-id="48e41-125">현재 진단 확장 구성 가져오기</span><span class="sxs-lookup"><span data-stu-id="48e41-125">Get current diagnostics extension configuration</span></span>
<span data-ttu-id="48e41-126">[Get-AzureServiceDiagnosticsExtension](/powershell/module/azure/get-azureservicediagnosticsextension?view=azuresmps-3.7.0) cmdlet을 사용하여 클라우드 서비스에 대한 현재 진단 구성을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48e41-126">Use the [Get-AzureServiceDiagnosticsExtension](/powershell/module/azure/get-azureservicediagnosticsextension?view=azuresmps-3.7.0) cmdlet to get the current diagnostics configuration for a cloud service.</span></span>

```powershell
Get-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```

## <a name="remove-diagnostics-extension"></a><span data-ttu-id="48e41-127">진단 확장 제거</span><span class="sxs-lookup"><span data-stu-id="48e41-127">Remove diagnostics extension</span></span>
<span data-ttu-id="48e41-128">클라우드 서비스에서 진단을 해제하려면 [Remove-AzureServiceDiagnosticsExtension](/powershell/module/azure/remove-azureservicediagnosticsextension?view=azuresmps-3.7.0) cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="48e41-128">To turn off diagnostics on a cloud service you can use the [Remove-AzureServiceDiagnosticsExtension](/powershell/module/azure/remove-azureservicediagnosticsextension?view=azuresmps-3.7.0) cmdlet.</span></span>

```powershell
Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```

<span data-ttu-id="48e41-129">*Role* 매개 변수 없이 *Set-AzureServiceDiagnosticsExtension* 또는 *New-AzureServiceDiagnosticsExtensionConfig*를 사용하여 진단 확장을 사용하도록 설정한 경우에는 *Role* 매개 변수 없이 *Remove-AzureServiceDiagnosticsExtension*을 사용하여 확장을 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48e41-129">If you enabled the diagnostics extension using either *Set-AzureServiceDiagnosticsExtension* or the *New-AzureServiceDiagnosticsExtensionConfig* without the *Role* parameter then you can remove the extension using *Remove-AzureServiceDiagnosticsExtension* without the *Role* parameter.</span></span> <span data-ttu-id="48e41-130">*Role* 매개 변수가 확장을 사용하도록 설정할 때 사용되었으면, 확장을 제거할 때도 사용되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="48e41-130">If the *Role* parameter was used when enabling the extension then it must also be used when removing the extension.</span></span>

<span data-ttu-id="48e41-131">각각의 개별 역할에서 진단 확장을 제거하려면:</span><span class="sxs-lookup"><span data-stu-id="48e41-131">To remove the diagnostics extension from each individual role:</span></span>

```powershell
Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService" -Role "WebRole"
```

## <a name="next-steps"></a><span data-ttu-id="48e41-132">다음 단계</span><span class="sxs-lookup"><span data-stu-id="48e41-132">Next Steps</span></span>
* <span data-ttu-id="48e41-133">문제 해결을 위한 Azure 진단 및 기타 기법 사용에 대한 추가 지침은 [Azure 클라우드 서비스 및 가상 컴퓨터에서 진단 사용](cloud-services-dotnet-diagnostics.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="48e41-133">For additional guidance on using Azure diagnostics and other techniques to troubleshoot problems, see [Enabling Diagnostics in Azure Cloud Services and Virtual Machines](cloud-services-dotnet-diagnostics.md).</span></span>
* <span data-ttu-id="48e41-134">[진단 구성 스키마](https://msdn.microsoft.com/library/azure/dn782207.aspx) 는 진단 확장에 대한 다양한 XML 구성 옵션을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="48e41-134">The [Diagnostics Configuration Schema](https://msdn.microsoft.com/library/azure/dn782207.aspx) explains the various xml configurations options for the diagnostics extension.</span></span>
* <span data-ttu-id="48e41-135">가상 컴퓨터에 대해 진단 확장을 사용하도록 설정하는 방법을 알아보려면 [Azure 리소스 관리자 템플릿을 사용한 모니터링 및 진단으로 Windows 가상 컴퓨터 만들기(영문)](../virtual-machines/windows/extensions-diagnostics-template.md)</span><span class="sxs-lookup"><span data-stu-id="48e41-135">To learn how to enable the diagnostics extension for Virtual Machines, see [Create a Windows Virtual machine with monitoring and diagnostics using Azure Resource Manager Template](../virtual-machines/windows/extensions-diagnostics-template.md)</span></span>
