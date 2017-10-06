---
title: "Azure에서 Application Insights aaaUsing PowerShell toosetup | Microsoft Docs"
description: "구성 Azure 진단 toopipe tooApplication 통찰력을 자동화 합니다."
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
ms.openlocfilehash: c48a5d8eb23df162522860935af876063aaa6976
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="using-powershell-tooset-up-application-insights-for-an-azure-web-app"></a><span data-ttu-id="2edad-103">Azure 웹 앱에 대 한 PowerShell tooset Application Insights를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="2edad-103">Using PowerShell tooset up Application Insights for an Azure web app</span></span>
<span data-ttu-id="2edad-104">[Microsoft Azure](https://azure.com) 수 [toosend Azure 진단 구성](app-insights-azure-diagnostics.md) 너무[Azure Application Insights](app-insights-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2edad-104">[Microsoft Azure](https://azure.com) can be [configured toosend Azure Diagnostics](app-insights-azure-diagnostics.md) too[Azure Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="2edad-105">hello 진단 tooAzure 클라우드 서비스 및 Azure Vm에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="2edad-105">hello diagnostics relate tooAzure Cloud Services and Azure VMs.</span></span> <span data-ttu-id="2edad-106">Hello Application Insights SDK를 사용 하 여 hello 앱 내에서 전송 하는 hello 원격 분석을 보완 합니다.</span><span class="sxs-lookup"><span data-stu-id="2edad-106">They complement hello telemetry that you send from within hello app using hello Application Insights SDK.</span></span> <span data-ttu-id="2edad-107">일부로 hello Azure에서 새 리소스를 만드는 과정을 자동화, PowerShell을 사용 하 여 진단을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2edad-107">As part of automating hello process of creating new resources in Azure, you can configure diagnostics using PowerShell.</span></span>

## <a name="azure-template"></a><span data-ttu-id="2edad-108">Azure 템플릿</span><span class="sxs-lookup"><span data-stu-id="2edad-108">Azure template</span></span>
<span data-ttu-id="2edad-109">Azure의 hello 웹 앱이 Azure 리소스 관리자 템플릿을 사용 하 여 리소스를 만들 경우에이 toohello 리소스 노드를 추가 하 여 Application Insights를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2edad-109">If hello web app is in Azure and you create your resources using an Azure Resource Manager template, you can configure Application Insights by adding this toohello resources node:</span></span>

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

* <span data-ttu-id="2edad-110">`nameOfAIAppResource`-hello Application Insights 리소스에 대 한 이름</span><span class="sxs-lookup"><span data-stu-id="2edad-110">`nameOfAIAppResource` - a name for hello Application Insights resource</span></span>
* <span data-ttu-id="2edad-111">`myWebAppName`-hello 웹 응용 프로그램의 hello id</span><span class="sxs-lookup"><span data-stu-id="2edad-111">`myWebAppName` - hello id of hello web app</span></span>

## <a name="enable-diagnostics-extension-as-part-of-deploying-a-cloud-service"></a><span data-ttu-id="2edad-112">클라우드 서비스 배포의 일부로 진단 확장을 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="2edad-112">Enable diagnostics extension as part of deploying a Cloud Service</span></span>
<span data-ttu-id="2edad-113">hello `New-AzureDeployment` cmdlet에 매개 변수가 `ExtensionConfiguration`, 진단 구성의 배열을 사용 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="2edad-113">hello `New-AzureDeployment` cmdlet has a parameter `ExtensionConfiguration`, which takes an array of diagnostics configurations.</span></span> <span data-ttu-id="2edad-114">Hello를 사용 하 여 만들 수 있습니다 `New-AzureServiceDiagnosticsExtensionConfig` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="2edad-114">These can be created using hello `New-AzureServiceDiagnosticsExtensionConfig` cmdlet.</span></span> <span data-ttu-id="2edad-115">예:</span><span class="sxs-lookup"><span data-stu-id="2edad-115">For example:</span></span>

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

## <a name="enable-diagnostics-extension-on-an-existing-cloud-service"></a><span data-ttu-id="2edad-116">기존 클라우드 서비스에 진단 확장을 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="2edad-116">Enable diagnostics extension on an existing Cloud Service</span></span>
<span data-ttu-id="2edad-117">기존 서비스에서 `Set-AzureServiceDiagnosticsExtension`을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2edad-117">On an existing service, use `Set-AzureServiceDiagnosticsExtension`.</span></span>

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

## <a name="get-current-diagnostics-extension-configuration"></a><span data-ttu-id="2edad-118">현재 진단 확장 구성 가져오기</span><span class="sxs-lookup"><span data-stu-id="2edad-118">Get current diagnostics extension configuration</span></span>
```ps

    Get-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```


## <a name="remove-diagnostics-extension"></a><span data-ttu-id="2edad-119">진단 확장 제거</span><span class="sxs-lookup"><span data-stu-id="2edad-119">Remove diagnostics extension</span></span>
```ps

    Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```

<span data-ttu-id="2edad-120">중 하나를 사용 하 여 hello 진단 확장을 사용 하는 경우 `Set-AzureServiceDiagnosticsExtension` 또는 `New-AzureServiceDiagnosticsExtensionConfig` hello 역할 매개 변수 없이 제거할 수 있습니다 사용 하 여 hello 확장 `Remove-AzureServiceDiagnosticsExtension` hello 역할 매개 변수 없이 합니다.</span><span class="sxs-lookup"><span data-stu-id="2edad-120">If you enabled hello diagnostics extension using either `Set-AzureServiceDiagnosticsExtension` or `New-AzureServiceDiagnosticsExtensionConfig` without hello Role parameter, then you can remove hello extension using `Remove-AzureServiceDiagnosticsExtension` without hello Role parameter.</span></span> <span data-ttu-id="2edad-121">Hello 역할 매개 변수는 hello 확장을 사용 하도록 설정할 때 사용 된 경우 다음도 수 사용 합니다 hello 확장명을 제거 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="2edad-121">If hello Role parameter was used when enabling hello extension then it must also be used when removing hello extension.</span></span>

<span data-ttu-id="2edad-122">각 개별 역할에서 tooremove hello 진단 확장:</span><span class="sxs-lookup"><span data-stu-id="2edad-122">tooremove hello diagnostics extension from each individual role:</span></span>

```ps

    Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService" -Role "WebRole"
```


## <a name="see-also"></a><span data-ttu-id="2edad-123">참고 항목</span><span class="sxs-lookup"><span data-stu-id="2edad-123">See also</span></span>
* [<span data-ttu-id="2edad-124">Application Insights로 Azure 클라우드 서비스 앱 모니터링</span><span class="sxs-lookup"><span data-stu-id="2edad-124">Monitor Azure Cloud Services apps with Application Insights</span></span>](app-insights-cloudservices.md)
* [<span data-ttu-id="2edad-125">Azure 진단 tooApplication Insights 보내기</span><span class="sxs-lookup"><span data-stu-id="2edad-125">Send Azure Diagnostics tooApplication Insights</span></span>](app-insights-azure-diagnostics.md)
* [<span data-ttu-id="2edad-126">구성 경고 자동화</span><span class="sxs-lookup"><span data-stu-id="2edad-126">Automate configuring alerts</span></span>](app-insights-powershell-alerts.md)

