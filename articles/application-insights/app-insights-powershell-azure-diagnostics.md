---
title: "Azure에서 PowerShell을 사용하여 Application Insights 설정 | Microsoft Docs"
description: "Application Insights에 대한 파이프에 Azure 진단 자동화 구성"
services: application-insights
documentationcenter: .net
author: sbtron
manager: carmonm
ms.assetid: 4ac803a8-f424-4c0c-b18f-4b9c189a64a5
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/17/2015
ms.author: bwren
ms.openlocfilehash: 3b6da89cc33cda713b483a2af3cbb493a03d6bec
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="using-powershell-to-set-up-application-insights-for-an-azure-web-app"></a><span data-ttu-id="240e5-103">PowerShell을 사용하여 Azure 웹앱에서 Application Insights 설정</span><span class="sxs-lookup"><span data-stu-id="240e5-103">Using PowerShell to set up Application Insights for an Azure web app</span></span>
<span data-ttu-id="240e5-104">[Microsoft Azure](https://azure.com)는 [Azure Application Insights](app-insights-overview.md)에 [Azure 진단을 보내도록 구성](app-insights-azure-diagnostics.md)될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="240e5-104">[Microsoft Azure](https://azure.com) can be [configured to send Azure Diagnostics](app-insights-azure-diagnostics.md) to [Azure Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="240e5-105">진단은 Azure 클라우드 서비스 및 Azure VM과 연관됩니다.</span><span class="sxs-lookup"><span data-stu-id="240e5-105">The diagnostics relate to Azure Cloud Services and Azure VMs.</span></span> <span data-ttu-id="240e5-106">이들 항목은 Application Insights SDK를 사용하여 앱 내부에서 보내는 원격 분석을 보완합니다.</span><span class="sxs-lookup"><span data-stu-id="240e5-106">They complement the telemetry that you send from within the app using the Application Insights SDK.</span></span> <span data-ttu-id="240e5-107">Azure에서 새 리소스 생성 과정에 대한 자동화의 일환으로 PowerShell을 사용하여 진단을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="240e5-107">As part of automating the process of creating new resources in Azure, you can configure diagnostics using PowerShell.</span></span>

## <a name="azure-template"></a><span data-ttu-id="240e5-108">Azure 템플릿</span><span class="sxs-lookup"><span data-stu-id="240e5-108">Azure template</span></span>
<span data-ttu-id="240e5-109">웹앱이 Azure에 있고 Azure Resource Manager 템플릿을 사용하여 리소스를 만드는 경우 리소스 노드에 이를 추가하여 Application Insights를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="240e5-109">If the web app is in Azure and you create your resources using an Azure Resource Manager template, you can configure Application Insights by adding this to the resources node:</span></span>

    {
      resources: [
        /* Create Application Insights resource */
        {
          "apiVersion": "2015-05-01",
          "type": "microsoft.insights/components",
          "name": "nameOfAIAppResource",
          "location": "centralus",
          "kind": "web",
          "properties": { "ApplicationId": "nameOfAIAppResource" },
          "dependsOn": [
            "[concat('Microsoft.Web/sites/', myWebAppName)]"
          ]
        }
       ]
     } 

* <span data-ttu-id="240e5-110">`nameOfAIAppResource` - Application Insights 리소스의 이름</span><span class="sxs-lookup"><span data-stu-id="240e5-110">`nameOfAIAppResource` - a name for the Application Insights resource</span></span>
* <span data-ttu-id="240e5-111">`myWebAppName` - 웹앱의 ID</span><span class="sxs-lookup"><span data-stu-id="240e5-111">`myWebAppName` - the id of the web app</span></span>

## <a name="enable-diagnostics-extension-as-part-of-deploying-a-cloud-service"></a><span data-ttu-id="240e5-112">클라우드 서비스 배포의 일부로 진단 확장을 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="240e5-112">Enable diagnostics extension as part of deploying a Cloud Service</span></span>
<span data-ttu-id="240e5-113">`New-AzureDeployment` cmdlet에는 `ExtensionConfiguration` 매개 변수가 있으며, 진단 구성의 배열을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="240e5-113">The `New-AzureDeployment` cmdlet has a parameter `ExtensionConfiguration`, which takes an array of diagnostics configurations.</span></span> <span data-ttu-id="240e5-114">이것은 `New-AzureServiceDiagnosticsExtensionConfig` cmdlet을 사용하여 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="240e5-114">These can be created using the `New-AzureServiceDiagnosticsExtensionConfig` cmdlet.</span></span> <span data-ttu-id="240e5-115">예:</span><span class="sxs-lookup"><span data-stu-id="240e5-115">For example:</span></span>

```ps

    $service_package = "CloudService.cspkg"
    $service_config = "ServiceConfiguration.Cloud.cscfg"
    $diagnostics_storagename = "myservicediagnostics"
    $webrole_diagconfigpath = "MyService.WebRole.PubConfig.xml" 
    $workerrole_diagconfigpath = "MyService.WorkerRole.PubConfig.xml"

    $primary_storagekey = (Get-AzureStorageKey `
     -StorageAccountName "$diagnostics_storagename").Primary
    $storage_context = New-AzureStorageContext `
       -StorageAccountName $diagnostics_storagename `
       -StorageAccountKey $primary_storagekey

    $webrole_diagconfig = `
     New-AzureServiceDiagnosticsExtensionConfig `
      -Role "WebRole" -Storage_context $storageContext `
      -DiagnosticsConfigurationPath $webrole_diagconfigpath
    $workerrole_diagconfig = `
     New-AzureServiceDiagnosticsExtensionConfig `
      -Role "WorkerRole" `
      -StorageContext $storage_context `
      -DiagnosticsConfigurationPath $workerrole_diagconfigpath

    New-AzureDeployment `
      -ServiceName $service_name `
      -Slot Production `
      -Package $service_package `
      -Configuration $service_config `
      -ExtensionConfiguration @($webrole_diagconfig,$workerrole_diagconfig)

``` 

## <a name="enable-diagnostics-extension-on-an-existing-cloud-service"></a><span data-ttu-id="240e5-116">기존 클라우드 서비스에 진단 확장을 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="240e5-116">Enable diagnostics extension on an existing Cloud Service</span></span>
<span data-ttu-id="240e5-117">기존 서비스에서 `Set-AzureServiceDiagnosticsExtension`을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="240e5-117">On an existing service, use `Set-AzureServiceDiagnosticsExtension`.</span></span>

```ps

    $service_name = "MyService"
    $diagnostics_storagename = "myservicediagnostics"
    $webrole_diagconfigpath = "MyService.WebRole.PubConfig.xml" 
    $workerrole_diagconfigpath = "MyService.WorkerRole.PubConfig.xml"
    $primary_storagekey = (Get-AzureStorageKey `
         -StorageAccountName "$diagnostics_storagename").Primary
    $storage_context = New-AzureStorageContext `
        -StorageAccountName $diagnostics_storagename `
        -StorageAccountKey $primary_storagekey

    Set-AzureServiceDiagnosticsExtension `
        -StorageContext $storage_context `
        -DiagnosticsConfigurationPath $webrole_diagconfigpath `
        -ServiceName $service_name `
        -Slot Production `
        -Role "WebRole" 
    Set-AzureServiceDiagnosticsExtension `
        -StorageContext $storage_context `
        -DiagnosticsConfigurationPath $workerrole_diagconfigpath `
        -ServiceName $service_name `
        -Slot Production `
        -Role "WorkerRole"
```

## <a name="get-current-diagnostics-extension-configuration"></a><span data-ttu-id="240e5-118">현재 진단 확장 구성 가져오기</span><span class="sxs-lookup"><span data-stu-id="240e5-118">Get current diagnostics extension configuration</span></span>
```ps

    Get-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```


## <a name="remove-diagnostics-extension"></a><span data-ttu-id="240e5-119">진단 확장 제거</span><span class="sxs-lookup"><span data-stu-id="240e5-119">Remove diagnostics extension</span></span>
```ps

    Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```

<span data-ttu-id="240e5-120">Role 매개 변수 없이 `Set-AzureServiceDiagnosticsExtension` 또는 `New-AzureServiceDiagnosticsExtensionConfig`를 사용하여 진단 확장을 사용하도록 설정했다면, Role 매개 변수 없이 `Remove-AzureServiceDiagnosticsExtension`을 사용하여 확장을 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="240e5-120">If you enabled the diagnostics extension using either `Set-AzureServiceDiagnosticsExtension` or `New-AzureServiceDiagnosticsExtensionConfig` without the Role parameter, then you can remove the extension using `Remove-AzureServiceDiagnosticsExtension` without the Role parameter.</span></span> <span data-ttu-id="240e5-121">Role 매개 변수가 확장을 사용하도록 설정할 때 사용되었으면, 확장을 제거할 때도 사용되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="240e5-121">If the Role parameter was used when enabling the extension then it must also be used when removing the extension.</span></span>

<span data-ttu-id="240e5-122">각각의 개별 역할에서 진단 확장을 제거하려면:</span><span class="sxs-lookup"><span data-stu-id="240e5-122">To remove the diagnostics extension from each individual role:</span></span>

```ps

    Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService" -Role "WebRole"
```


## <a name="see-also"></a><span data-ttu-id="240e5-123">참고 항목</span><span class="sxs-lookup"><span data-stu-id="240e5-123">See also</span></span>
* [<span data-ttu-id="240e5-124">Application Insights로 Azure 클라우드 서비스 앱 모니터링</span><span class="sxs-lookup"><span data-stu-id="240e5-124">Monitor Azure Cloud Services apps with Application Insights</span></span>](app-insights-cloudservices.md)
* [<span data-ttu-id="240e5-125">Application Insights에 Azure 진단 보내기</span><span class="sxs-lookup"><span data-stu-id="240e5-125">Send Azure Diagnostics to Application Insights</span></span>](app-insights-azure-diagnostics.md)
* [<span data-ttu-id="240e5-126">구성 경고 자동화</span><span class="sxs-lookup"><span data-stu-id="240e5-126">Automate configuring alerts</span></span>](app-insights-powershell-alerts.md)

