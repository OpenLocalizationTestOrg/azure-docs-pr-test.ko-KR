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
# <a name="using-powershell-tooset-up-application-insights-for-an-azure-web-app"></a>Azure 웹 앱에 대 한 PowerShell tooset Application Insights를 사용 하 여
[Microsoft Azure](https://azure.com) 수 [toosend Azure 진단 구성](app-insights-azure-diagnostics.md) 너무[Azure Application Insights](app-insights-overview.md)합니다. hello 진단 tooAzure 클라우드 서비스 및 Azure Vm에 연결합니다. Hello Application Insights SDK를 사용 하 여 hello 앱 내에서 전송 하는 hello 원격 분석을 보완 합니다. 일부로 hello Azure에서 새 리소스를 만드는 과정을 자동화, PowerShell을 사용 하 여 진단을 구성할 수 있습니다.

## <a name="azure-template"></a>Azure 템플릿
Azure의 hello 웹 앱이 Azure 리소스 관리자 템플릿을 사용 하 여 리소스를 만들 경우에이 toohello 리소스 노드를 추가 하 여 Application Insights를 구성할 수 있습니다.

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

* `nameOfAIAppResource`-hello Application Insights 리소스에 대 한 이름
* `myWebAppName`-hello 웹 응용 프로그램의 hello id

## <a name="enable-diagnostics-extension-as-part-of-deploying-a-cloud-service"></a>클라우드 서비스 배포의 일부로 진단 확장을 사용하도록 설정
hello `New-AzureDeployment` cmdlet에 매개 변수가 `ExtensionConfiguration`, 진단 구성의 배열을 사용 하는 합니다. Hello를 사용 하 여 만들 수 있습니다 `New-AzureServiceDiagnosticsExtensionConfig` cmdlet. 예:

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

## <a name="enable-diagnostics-extension-on-an-existing-cloud-service"></a>기존 클라우드 서비스에 진단 확장을 사용하도록 설정
기존 서비스에서 `Set-AzureServiceDiagnosticsExtension`을 사용합니다.

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

## <a name="get-current-diagnostics-extension-configuration"></a>현재 진단 확장 구성 가져오기
```ps

    Get-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```


## <a name="remove-diagnostics-extension"></a>진단 확장 제거
```ps

    Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```

중 하나를 사용 하 여 hello 진단 확장을 사용 하는 경우 `Set-AzureServiceDiagnosticsExtension` 또는 `New-AzureServiceDiagnosticsExtensionConfig` hello 역할 매개 변수 없이 제거할 수 있습니다 사용 하 여 hello 확장 `Remove-AzureServiceDiagnosticsExtension` hello 역할 매개 변수 없이 합니다. Hello 역할 매개 변수는 hello 확장을 사용 하도록 설정할 때 사용 된 경우 다음도 수 사용 합니다 hello 확장명을 제거 하는 경우.

각 개별 역할에서 tooremove hello 진단 확장:

```ps

    Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService" -Role "WebRole"
```


## <a name="see-also"></a>참고 항목
* [Application Insights로 Azure 클라우드 서비스 앱 모니터링](app-insights-cloudservices.md)
* [Azure 진단 tooApplication Insights 보내기](app-insights-azure-diagnostics.md)
* [구성 경고 자동화](app-insights-powershell-alerts.md)

